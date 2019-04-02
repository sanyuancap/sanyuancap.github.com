# js 和min.js的区别

    js是JavaScript 源码文件
    .min.js是压缩版的js文件。

## 为什么要压缩？
 - 减小体积

.min.js文件经过压缩，相对编译前的js文件体积较小，传输效率快。
 - 防止窥视和窃取源代码

经过编码将变量和函数原命名改为毫无意义的命名，以防止他人窥视和窃取 js 源代码

## 压缩原理？

删除 js 代码中所有注释、跳格符号、换行符号及无用的空格，从而压缩 
JS 文件大小。

    混淆：经过编码将变量和函数原命名改为毫无意义的命名，删除无用代码，内联函数，等价语句替换等(以防止他人窥视和窃取源码)

## 压缩工具
 
[JavaScript Minifier][2]
 
[更多资料][1]

[1]: http://www.php.cn/js-tutorial-390918.html
[2]: http://www.cnblogs.com/lhb25/p/15-best-javascript-minifying-tools.html
