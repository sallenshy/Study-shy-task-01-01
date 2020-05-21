# 宋杭原｜ Part 1 | 模块一
###第一题

    const a  = []
    for (var i = 0 ;i<10 ;i++)
    {
	    a[i] = function(){
		   console.log(i)
	    }
    }
    a[6]();
    
最终执行结果为：打印出 10。

原因逐行分析：
1： 声明常量 a 为一个数组
2：for循环 10次   a[i] = function(){}  表示 数组里每一个元素都是一个函数方法
3：for循环时 变量i 用var关键字声明 在函数作用域中   所以循环结束后 i的值依次从0变成了10  最后的值就是10 如将var改成let 则i的值是在每个块级作用域中，都是不一样的。
4：所以执行a[6] 数组中第7个元素（函数方法）就是打印常量i的值 此时为10

### 第二题
说出下列的执行结果并解释

    var tem = 123
    if(true){
	    console.log(tem);
	    let tem;
    }
最终执行结果 程序报错
1：var 声明tem变量 123 
2：在当前块级作用域中 存在let声明 对于区块外的变量是不能使用的 
3： 又因为let声明不会做变量提升，此时的块级作用域中的tem是未被初始化的，所以就会报错

### 第三题
结合ES6新语法 找出数组中最小的值

    var arr = [12,34,32,89,4]
    
解：

    const minNum = Math.min(...arr)

### 第四题
详细说明let var 和 const 三种声明变量方式的之间具体差别

答：
1：let const 不能跨块访问 var可以
2：let  var 声明变量不需要初始化 const声明必须初始化，const是指针，不能更改指向 定义的变量不能重新赋值 如果是对象类型的话 可以修改对象属性
3： var 存在变量提升 let const则不存在

### 第五题
请说出下面代码的执行结果，并解释

    var a = 10
    var obj = {
	    a:20,
	    fn(){
	        setTimeout(()=>{
	            console.log(this.a)
	        })
		}
	}
	obj.fn();

运行结果为 20
分析：
1：声明常量a=10
2：声明obj对象  对象属性 一个属性名a值为20， 一个属性名fn的函数方法 
3：函数方法内使用箭头函数，不会指向this的指向 当前谁调用就是指向谁 所以this指向的是obj对象  this.a == obj.a  输出结果为20

### 第六题
简述Symbol类型的用途
答：
1：可以表示一个独一无二的值
2：可用做类成员的私有化
3：可迭代

### 第七题
说说什么是浅拷贝，什么是深拷贝
答：
浅拷贝和深拷贝只是针对引用类型 即保存在堆内存空间中
浅拷贝就是复制指针，和原指针同时指向同一块内存空间，所以当改变任何一个指针指向的内存空间数据时，新旧对象的数据都会改变
深拷贝是复制一个对象，不共享内存空间，新旧对象指针指向不同的内存空间，任何一方变化，都不会引起另一方的改变

### 第八题
如何理解JS异步编程，Event Loop是做什么，什么是宏任务，什么是微任务
答：
JS是单线程执行代码，为了解决耗时任务阻塞执行操作，JS有两种模式，一种为同步模式，一种是异步模式。同步模式将同步的API压入进栈，异步模式就是将开启或执行异步的API放到消息队列中去，然后根据Event Loop 监视消息队列和任务栈，一旦任务栈执行完毕，根据消息队列的执行情况再将API压入栈执行。
宏任务：回调队列中的任务 ，如script,setTimeout,setInterval
微任务：在宏任务执行过程中，临时增加的需求，当前任务结束后立即执行。如Promise,process.nextTick,MutationOberserver

### 第九题
下列异步代码使用promise改进

    setTimeout(function(){
	    var a = "hello";
	    setTimeout(function(){
	        var b = "lagou";
	        setTimeout(function(){
	            var c= "I ❤ U";
	            console.log(a + b + c);
	        },10)
	    },10)
	},10)
	
改：

    const pro = function(str){
	    return new Promise(function(resolve,reject){
	        setTimeout(function(){
	            resolve(str)
	        },10)
	        reject()
	    })
	}
	pro("hello").then(function(a){
	    var b = "lagou"
	    pro(b).then(function(b){
	        var c= "I ❤ U";
	        pro(c).then(function(c){
            console.log(a+b+c)
	        })
	    })
	})

### 第十题
简述TypeScript和JavaScript的关系
答：
TypeScript是Javascript的超集 

### 第十一题
谈谈TypeScript的优缺点
答：
优点：
1：功能强大，增加了代码的可读性和可维护性
2：生态环境强大
3：包容性强，适用所有的Js环境
缺点：
1.学习成本较高，新增很多类型和概念
2对于小型项目，构建成本高
