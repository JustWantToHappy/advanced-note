require导入才会执行模块代码，require本质上是一个函数，如下是一个require函数的伪代码
```javascript
const require=(modulePath)=>{
    //根据传递的模块路径，得到模块完整的绝对路径
    var moduleId=getModuleId(modulePath)
    //判断缓存
    if(cached[moduleId]){
        return cached[moduleId]
    }
    //真正运行模块代码的辅助函数
    //这些参数就解释了为什么在commonjs的模块中可以直接使用exports,module.exports,__dirname等等
    function __require(exports,require,module,__filename,__dirname){
        //真正运行的代码,require的内容就会在这里面执行
    }
    var module={
        exports:{}
    }
    var exports=module.exports;
    var __filename=moduleId;
    __require.call(exports,exports,require,module,__filename,__dirname);
    cached[moduleId]=module.exports;
    return cached[moduleId];
}

```