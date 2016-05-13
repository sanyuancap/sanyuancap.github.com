---
layout: post
title: "unsynchronize pthread"
description: ""
category: 
tags: []
---
{% include JB/setup %}

    //主程序调用
    CCTextureCache::sharedTextureCache()->addImageAsync("Images/HelloWorld.png", this, callfuncO_selector(TextureCacheTest::loadingCallBack));
    CCTextureCache::sharedTextureCache()->addImageAsync("Images/grossini.png", this, callfuncO_selector(TextureCacheTest::loadingCallBack));
    void TextureCacheTest::loadingCallBack(CCObject *obj)
    {
        ++m_nNumberOfLoadedSprites;
        char tmp[10];
        sprintf(tmp,"%%%d", (int)(((float)m_nNumberOfLoadedSprites / m_nNumberOfSprites) * 100));
        m_pLabelPercent->setString(tmp);
        if (m_nNumberOfLoadedSprites == m_nNumberOfSprites)
        {
            this->removeChild(m_pLabelLoading, true);
            this->removeChild(m_pLabelPercent, true);
            addSprite();
        }
    }

--- 

    //CCTextureCache.cpp
    void CCTextureCache::addImageAsync(const char *path, CCObject *target, SEL_CallFuncO selector)
    {
    #ifdef EMSCRIPTEN
        CCLOGWARN("Cannot load image %s asynchronously in Emscripten builds.", path);
        return;
    #endif // EMSCRIPTEN
        CCAssert(path != NULL, "TextureCache: fileimage MUST not be NULL");    
        CCTexture2D *texture = NULL;
        // optimization
        std::string pathKey = path;
        pathKey = CCFileUtils::sharedFileUtils()->fullPathForFilename(pathKey.c_str());
        texture = (CCTexture2D*)m_pTextures->objectForKey(pathKey.c_str());
        std::string fullpath = pathKey;
        if (texture != NULL)
        {
            if (target && selector)
            {
                (target->*selector)(texture);
            }
            
            return;
        }


        // lazy init
        if (s_pAsyncStructQueue == NULL)
        {             
            s_pAsyncStructQueue = new queue<AsyncStruct*>();
            s_pImageQueue = new queue<ImageInfo*>();        
            
            pthread_mutex_init(&s_asyncStructQueueMutex, NULL);
            pthread_mutex_init(&s_ImageInfoMutex, NULL);
            pthread_mutex_init(&s_SleepMutex, NULL);
            pthread_cond_init(&s_SleepCondition, NULL);
    #if (CC_TARGET_PLATFORM != CC_PLATFORM_WINRT) && (CC_TARGET_PLATFORM != CC_PLATFORM_WP8)
            pthread_create(&s_loadingThread, NULL, loadImage, NULL);
    #endif
            need_quit = false;
        }

        if (0 == s_nAsyncRefCount)
        {
            CCDirector::sharedDirector()->getScheduler()->scheduleSelector(schedule_selector(CCTextureCache::addImageAsyncCallBack), this, 0, false);
        }

        ++s_nAsyncRefCount;

        if (target)
        {
            target->retain();
        }

        // generate async struct
        AsyncStruct *data = new AsyncStruct();
        data->filename = fullpath.c_str();
        data->target = target;
        data->selector = selector;

    #if (CC_TARGET_PLATFORM != CC_PLATFORM_WINRT) && (CC_TARGET_PLATFORM != CC_PLATFORM_WP8)
        // add async struct into queue
        pthread_mutex_lock(&s_asyncStructQueueMutex);
        s_pAsyncStructQueue->push(data);
        pthread_mutex_unlock(&s_asyncStructQueueMutex);
        pthread_cond_signal(&s_SleepCondition);
    #else
        // WinRT uses an Async Task to load the image since the ThreadPool has a limited number of threads
        //std::replace( data->filename.begin(), data->filename.end(), '/', '\\'); 
        create_task([this, data] {
            loadImageData(data);
        });
    #endif
    }

    void CCTextureCache::addImageAsyncCallBack(float dt)
    {
        // the image is generated in loading thread
        std::queue<ImageInfo*> *imagesQueue = s_pImageQueue;

        pthread_mutex_lock(&s_ImageInfoMutex);
        if (imagesQueue->empty())
        {
            pthread_mutex_unlock(&s_ImageInfoMutex);
        }
        else
        {
            ImageInfo *pImageInfo = imagesQueue->front();
            imagesQueue->pop();
            pthread_mutex_unlock(&s_ImageInfoMutex);

            AsyncStruct *pAsyncStruct = pImageInfo->asyncStruct;
            CCImage *pImage = pImageInfo->image;

            CCObject *target = pAsyncStruct->target;
            SEL_CallFuncO selector = pAsyncStruct->selector;
            const char* filename = pAsyncStruct->filename.c_str();

            // generate texture in render thread
            CCTexture2D *texture = new CCTexture2D();
    #if 0 //TODO: (CC_TARGET_PLATFORM == CC_PLATFORM_IOS)
            texture->initWithImage(pImage, kCCResolutioniPhone);
    #else
            texture->initWithImage(pImage);
    #endif

    #if CC_ENABLE_CACHE_TEXTURE_DATA
           // cache the texture file name
           VolatileTexture::addImageTexture(texture, filename, pImageInfo->imageType);
    #endif

            // cache the texture
            m_pTextures->setObject(texture, filename);
            texture->autorelease();

            if (target && selector)
            {
                (target->*selector)(texture);
                target->release();
            }        

            pImage->release();
            delete pAsyncStruct;
            delete pImageInfo;

            --s_nAsyncRefCount;
            if (0 == s_nAsyncRefCount)
            {
                CCDirector::sharedDirector()->getScheduler()->unscheduleSelector(schedule_selector(CCTextureCache::addImageAsyncCallBack), this);
            }
        }
    }