自定义构造函数（必须用new 调用不然与普通函数没什么区别）
什么是构造函数？--------用来初始化对象（给对象添加属性或者方法）

function Person(name, age, job){
// 
  this.name = name;
  this.age = age;
  this.job= job;
  this.sayName = function(){
    console.log(this.name);
  }
}
var person1 = new Person("tt",11,"teacher");
new 创建新对象
通过new操作符来调用会经过以下几个步骤：
1、新建一个空对象
var person1 = new object();
2、调用构造函数，把新创建的对象赋值给构造函数中的this
3、执行构造函数时（使用this）给新对象添加属性和方法
4、返回新创建对象



关于构造函数的返回值：
1、默认返回来的是新建对象
2、如果自己添加了return(return;)+基本类型值依旧只返回新创建的对象
3、如果是return+object类型值不会返回新创建的对象，返回的则是return后面的对象

