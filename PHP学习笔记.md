# PHP学习笔记

## php博客系统开发

​							http://www.maiziedu.com/course/333/







## php 上传文件导致fetch_assoc() on boolean 报错

​		Call to a member function xxxxx() on boolean，在一个布尔型变量上调用一个方法。
错不是该方法的错，是查询的错。所以这个错误提示看不出来什么问题。要看到查询错误的提示，用mysqli->error返回错误提示，然后echo输出看看是什么错误



## JavaScript 获取当前时间戳


```javascript
第一种方法：

var timestamp = Date.parse(new Date());

结果：1280977330000
第二种方法：

var timestamp = (new Date()).valueOf();

结果：1280977330748

第三种方法：

var timestamp=new Date().getTime()；

结果：1280977330748
```



## [Field 'id' doesn't have a default value?](http://stackoverflow.com/questions/25865104/field-id-doesnt-have-a-default-value)

​	MySQL is most likely in **STRICT** sql mode. Try to execute sql query *SET GLOBAL sql_mode=''* or edit your **my.cnf** / **my.ini** to make sure you aren't setting *STRICT_ALL_TABLES* and/or*STRICT_TRANS_TABLES*.

​	Delet  *STRICT_ALL_TABLES* and/or*STRICT_TRANS_TABLES* in **my.ini** and You can fix this problem . 



## 在PHP语言中使用JSON

​	http://www.ruanyifeng.com/blog/2011/01/json_in_php.html

​	**json_encode()**

​	注意，数据格式从"[]"（数组）变成了"{}"（对象）。

​	如果你需要将"索引数组"强制转化成"对象"，可以这样写

> ```
> 　　json_encode( (object)$arr );
> 　　
>
> ```

或者

> ```
> 　　json_encode ( $arr, JSON_FORCE_OBJECT );
> 　　
> ```
