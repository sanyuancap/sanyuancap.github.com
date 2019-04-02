new Promise((resolve, reject) => {
    
.then(()

// bad
array.map(x=>x + 1);
array.map(x => {
   return x + 1;
});

// good
array.map(x => x + 1);


vue 双花括号:执行表达式,将表达式的结果 输出到当前调用的元素的innerHTML中


HTML内容模板（<template>）元素是一种用于保存客户端内容机制，该内容在加载页面时不会呈现，但随后可以在运行时使用JavaScript实例化。

将模板视为一个内容片段，存储在文档中供后续使用。虽然解析器在加载页面时确实会处理<template>元素的内容，但这样做只是为了确保这些内容有效；然而，元素的内容不会被呈现。



try 
{  
if(typeof(eval(funcName))=="function")  
{  
funcName();  
}  
}catch(e)  
{  
alert("not function");  
}   


function check()  
{  
if (typeof(myvalue)=="undefined")  
{  
alert("value is undefined");  
}  
else 
{  
alert("value is true");  
}  
}



js 参数传递

：

this.answerQuestion({
                is_correct,
                idx,
                courseware_question_number,
            }).then((res) => {
                cc.log('答题统计返回', res);
            }).catch((err) => {
                if (err) {
                    // 请求错误
                    cc.error(err);
                    this.showMask('hide');
                }
            });



5.forEach不允许return？？
unsyntactic break

rightAnswersArr.forEach((value,index)=>{
    if(rightAnswersArr[index] !== fillAnswersArr[index]) {
        isEqual = false;
    }
})


JS中的！=、== 、！==、===的用法和区别。

var num = 1;
 
var str = '1';
 
var test = 1;
 
test == num   //true　相同类型　相同值
 
test === num  //true　相同类型　相同值
 
test !== num  //false test与num类型相同，其值也相同,　非运算肯定是false
 
 
num == str   //true 　把str转换为数字，检查其是否相等。
 
num != str   //false  == 的 非运算
 
num === str  //false  类型不同，直接返回false
 
num !== str  //true   num 与 str类型不同 意味着其两者不等　非运算自然是true啦
== 和 != 比较若类型不同，先偿试转换类型，再作值比较，最后返回值比较结果 。
而 
=== 和 !== 只有在相同类型下,才会比较其值。
