---
layout: post
title: "cocos2dx学习之CCTextureCache"
description: ""
category: cocos2dx
tags: [cocos2dx,CCTextureCache]
---
{% include JB/setup %}

CCTextureCache原理大致分几步：

 1. 创建线程，用于后台加载
 2. 将对于需要加载的图片放入队列中
 3. callback函数设定，用于将加载完成的图片转为纹理，等待使用其调用是由CCTimer::update调用的。
 4. addImageAsyncCallBack函数在处理完纹理转换，还会调用addImageAsync传入的SEL_CallFuncO selector，实现用户加载图片纹理之后的具体处理。
    
        voidCCTextureCache::addImageAsync(constchar *path, CCObject *target, SEL_CallFuncO selector){
            CCAssert(path != NULL, "TextureCache: fileimage MUST not be NULL"); 
            CCTexture2D *texture = NULL;
        
            // optimization
            std::string pathKey = path;
            CCFileUtils::ccRemoveHDSuffixFromFile(pathKey);
        
            pathKey = CCFileUtils::fullPathFromRelativePath(pathKey.c_str());
            texture = m_pTextures->objectForKey(pathKey); //根据pathkey查看是否纹理已经加载过，如果已经有了，则不重复加载
            std::string fullpath = pathKey;
            if (texture != NULL)
            {
                if (target && selector)
                {
                    (target->*selector)(texture);
                }
                
                return;
            }
               if (target)
            {
                target->retain();
            }
        
            // lazy init
            static bool firstRun = true;
            if (firstRun)
            {            
                s_pAsyncStructQueue = new queue<AsyncStruct*>();
                s_pImageQueue = new queue<ImageInfo*>();        
        
                pthread_mutex_init(&s_asyncStructQueueMutex, NULL);
                sem_init(&s_sem, 0, 0);
                pthread_mutex_init(&s_ImageInfoMutex, NULL);
                pthread_create(&s_loadingThread, NULL, loadImage, NULL);//创建新的线程，用于后台加载图片

                //创建调度队列，用来根据已加载的图片进行纹理转换
                CCScheduler::sharedScheduler()->scheduleSelector(schedule_selector(CCTextureCache::addImageAsyncCallBack), this, 0, false);
                need_quit = false;
                firstRun = false;
            }
        
            // generate async struct
            AsyncStruct *data = new AsyncStruct();
            data->filename = fullpath.c_str();
            data->target = target;
            data->selector = selector;
        
            // add async struct into queue
            pthread_mutex_lock(&s_asyncStructQueueMutex);
            s_pAsyncStructQueue->push(data);//将需要加载的图片放入队列中
            pthread_mutex_unlock(&s_asyncStructQueueMutex);
        
            sem_post(&s_sem);
        }
        
[参考文章][1]


  [1]: http://www.cnblogs.com/SeanLin/archive/2012/03/15/2398190.html