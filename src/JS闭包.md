####  JS闭包

##### 什么是JS闭包

​        闭包是指有权访问另外一个函数作用域中的变量的函数

​	特点：

​		1.  函数

​		2.  能访问另外一个函数作用域中的变量

​	具体代码：

```javascript
	function getName() { 
      var name = "美女的名字";
      function displayName() {  
        console.log(name);   
      }  
      return displayName;
	}
    var girlName = getName();  
    girlName()  //"美女的名字"
```

##### 闭包的可以做些什么

​	1. 闭包可以访问当前函数以外的变量

​	2. 即使外部函数已经返回，闭包仍能访问外部函数定义的变量

​	3. 在内存中维持变量

​	4. 保护函数内的变量安全

##### 相关链接

1. <http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html>
2. <http://blog.csdn.net/sunlylorn/article/details/6534610>
3. <https://www.cnblogs.com/xxcanghai/p/4991870.html>


