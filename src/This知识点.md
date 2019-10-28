##参考资料
http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html

##1.this是什么
    this代表函数运行时，自动生成的一个内部对像，只能在函数内部使用。

##2.调用类型/用法
   1) 纯粹的函数调用/独立函数调用
   2) 作为对象方法的调用
   3) 作为构造函数调用
   4) apply/call调用

##3.绑定规则
#### 1)默认绑定
    function foo() {
        console.log(this.a);
    }
    var a = 2;
    foo();
    声明在全局作用域中的变量就是全局对象的一个同名属性；
    独立函数调用时，应用this的默认绑定，this就指向全局对象;
    如果使用严格模式，全局对象无法使用默认绑定，this会绑定到undefined
####2)隐式绑定
    var obj = {
        a: 2,
        foo: foo
    };
    obj.foo();
    this隐式绑定到拥有或者包含它的对象，即它的调用对象
####3)显示绑定
    可以使用call和apply方;

    foo.call(obj);
    在调用函数foo时，强制并显示的把它的this绑定到obj对象上
####4)硬绑定
    显示绑定的一个变种，可以解决绑定丢失的问题;
    var bar = obj.foo;
    bar();  // this的绑定丢失了
    ES5中可使用内置方法Function.prototype.bind实现硬绑定;
####5)new绑定
   const o = new obj();
   新对象会绑定到行数调用的this上

   优先级
   显示绑定(硬绑定) > new绑定 > 隐式绑定 > 默认绑定
   -- new 和 call/apply无法一起使用

-------------------------------------------------------------------------------
##总结

   判断this
    现在我们可以根据优先级来判断函数在某个调用位置应用的是哪条规则。可以按照下面的
    顺序来进行判断：
    1. 函数是否在new 中调用（new 绑定）？如果是的话this 绑定的是新创建的对象。
    var bar = new foo()
    2. 函数是否通过call、apply（显式绑定）或者硬绑定调用？如果是的话，this 绑定的是
    指定的对象。
    var bar = foo.call(obj2)
    3. 函数是否在某个上下文对象中调用（隐式绑定）？如果是的话，this 绑定的是那个上
    下文对象。
    var bar = obj1.foo()
    4. 如果都不是的话，使用默认绑定。如果在严格模式下，就绑定到undefined，否则绑定到
    全局对象。
    var bar = foo()

-------------------------------------------------------------------------------


##4.例外
   1)this被忽略
    call/apply中传入null或undefined,使用的是默认绑定，而非显示绑定
   2)间接引用
   3)软绑定

