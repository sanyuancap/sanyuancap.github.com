# Webpack学习

 - 什么是Webpack

WebPack可以看做是模块打包机

它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），并将其转换和打包为合适的格式供浏览器使用。

 - 一个常见的`webpack`配置文件

        const webpack = require('webpack');
        const HtmlWebpackPlugin = require('html-webpack-plugin');
        const ExtractTextPlugin = require('extract-text-webpack-plugin');

        module.exports = {
                entry: __dirname + "/app/main.js", //已多次提及的唯一入口文件
                output: {
                    path: __dirname + "/build",
                    filename: "bundle-[hash].js"
                },
                devtool: 'none',
                devServer: {
                    contentBase: "./public", //本地服务器所加载的页面所在的目录
                    historyApiFallback: true, //不跳转
                    inline: true,
                    hot: true
                },
                module: {
                    rules: [{
                            test: /(\.jsx|\.js)$/,
                            use: {
                                loader: "babel-loader"
                            },
                            exclude: /node_modules/
                        }, {
                            test: /\.css$/,
                            use: ExtractTextPlugin.extract({
                                fallback: "style-loader",
                                use: [{
                                    loader: "css-loader",
                                    options: {
                                        modules: true,
                                        localIdentName: '[name]__[local]--[hash:base64:5]'
                                    }
                                }, {
                                    loader: "postcss-loader"
                                }],
                            })
                        }
                    }
                ]
            },
            plugins: [
                new webpack.BannerPlugin('版权所有，翻版必究'),
                new HtmlWebpackPlugin({
                    template: __dirname + "/app/index.tmpl.html" //new 一个这个插件的实例，并传入相关的参数
                }),
                new webpack.optimize.OccurrenceOrderPlugin(),
                new webpack.optimize.UglifyJsPlugin(),
                new ExtractTextPlugin("style.css")
            ]
        };

 - Webpack的工作方式

把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。

 - Grunt以及Gulp

Gulp/Grunt是一种能够优化前端的开发流程的工具，而WebPack是一种模块化的解决方案

 - Grunt和Gulp的工作方式是：
 
在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的具体步骤，工具之后可以自动替你完成这些任务。
    
 - Webpack vs Grunt和Gulp
    
Webpack的处理速度更快更直接，能打包更多不同类型的文件。

 - Webpack 结构

        Entry: 入口
        Module：模块，webpack中一切皆模块，一个模块对应一个文件。webpack会从配置的Entry开始递归的找出所有依赖的模块。
        Chunk：代码块，一个Chunk由多个模块组成，用于代码合并和分割。
        Loader：webpack默认只能识别js模块，loader可以告诉webpack遇到不同类型模块要怎么处理。
        webpack不能识别非js结尾的模块，通过loader让webpack识别出来. 常用Loader
        编译相关： babel-loader、ts-loader
        样式相关： style-loader、css-loader、less-loader、 postcss-loader
        文件相关：file-loader、url-loader
        Plugin：扩展插件，构建流程中特定时机注入拓展逻辑，来改变构建结果或我们想要的事情
        Output：输出结果

 - webpack 4.x新特性

1. mode
2. 废弃了CommonsChunkPlugin
3. 只会对按需加载的代码做分割
4. extract-text-webpack-plugin 替换为 mini-css-extract-plugin

 - 一些工具

webpack-bundle-analyzer

    Webpack 插件和 CLI 实用程序，她可以将打包后的内容束展示为方便交互的直观树状图，让你明白你所构建包中真正引入的内容；我们可以借助她，发现它大体有哪些模块组成，找到不合时宜的存在，然后优化它。

speed-measure-webpack-plugin 

    对打包过程中消耗的时间进行精确的统计

 - 打包速度优化

跟上技术的迭代，升级node、npm、webpack（每次更新都会做一些优化，node升级运行效率提升，并且webpack运行在node环境, 新npm可以更快分析包依赖、包的引入，使得模块之间相互引用速度更快）
在尽可能少的模块应用Loader（等同于无谓的代码分析越少），合理使用exclude或include可以降低loader执行频率，从而提高打包速度

1. 合理使用sourceMap
2. 代码分割(code spliting)
3. Tree Shaking
4. Scope Hoisting
5. 使用dllPlugin优化打包
6. happypack多进程打包
7. 给loader更明确的指示（缩小文件的搜索范围）

[webpack简介][1]

[1]: https://segmentfault.com/a/1190000006178770#articleHeader6
