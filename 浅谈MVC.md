# 《浅谈MVC》
>>这两天学习了MVC，按照惯例写篇博客总结一下。
## 何为MVC
MVC是一种设计模式，它把系统分成三层：Model数据、View视图和Controller控制器。
这个模式认为，程序不论简单或复杂，从结构上看，都可以分成三层。
<blockquote>
// View：是这个js模块对应在html中的部分，就是展示给用户看的那一部分  
  
// Model：可以从服务器获得数据，把数据传给Controller。还要将Controller监听到的用户提交的数据上传到服务器。    
// Controller：调用model的数据，用来更新view。还要监听用户在view上的操作，获取用户提交的数据，传给model。
</blockquote>

```
Model 主要负责 AJAX 请求或者 LocalStorage 存储。
const m = {
    data: {程序需要操作的数据或信息},
    create() {增 },
    delete() { 删},
    update() {改},
    get() {查}
}
View 负责用户界面，前端 View 主要负责 HTML 渲染。
const v = {
    el: null,
    // 初始化html
    html: `呈现在页面上的html内容`
    init(container) {
        v.el = $(container)
    },
    render() {渲染页面}
}
Controller 控制器主要是打杂的，
1.将content塞到页面里
2.浏览器事件监听 - 用户点击视图后去更新数据（如 user）
3.数据事件监听 - user 数据更新后去更新视图
const c = {
    init(container) {})
    }, 
    events: { 事件}, 
    add() {详细执行},
    minus() {详细执行},
    mul() {详细执行},
    div() {详细执行},
    autoBindEvents() {逻辑}
    }
```
## EventBus 
EventBus也是一种设计模式或框架，它能够简化各组件间的通信，让我们的代码书写变得简单，能有效的分离事件发送方和接收方(也就是解耦的意思)，能避免复杂和容易出错的依赖性和生命周期问题。  

**EventBus的一些常用api**
* on（监听事件）
```
this.on('m:updated', () => {
      this.render(this.data)
    })
```
* trigger（触发事件）
```
update(data) {
    Object.assign(m.data, data)//把传进来的data直接放在m.data上
    eventBus.trigger('m:updated')//通过trigger自动更新数据
    localStorage.setItem('n', m.data.n)//储存数据
```
* off（取消监听）
  
## 表驱动编程（Table-Driven Methods）
表驱动法是一种编程模式，它可以将诸多事件进行简化的一种写法，因为这些事件涉及到很多的代码重复问题。
```angular2
//举个栗子
菜鸟的写法
if(month == 1)
        days =31;
     else if(month == 2)
        days = 29;
     else if
        ....
表驱动的写法
   months[12] = {31,29,31,30,31,30,31,31,30...};
   days = months[month -1];

```
## 我对模块化的理解
如果只是写一个简简单单的静态小页面，代码量只有几十行那种，那根本用不着搞什么模块化，但现在web前端已经演变成大前端，项目越来越复杂，代码量越来越多。
在这种情况下，学习模块化编程思想就显得尤为重要。
### 那何为模块化呢？
模块化是一种将系统分离成独立功能部分的方法，可将系统分割成独立的功能部分，严格定义模块接口、模块间具有透明性。
### 模块化有哪些优点：
* 可维护性（要是代码没有分模块全都堆在一起，出问题了，你找都不好找）
* 方便模块间组合、分解
* 方便单个模块功能调试、升级
* 多人协作互不干扰
* 可以分开做测试，简化测试
* 避免重复造轮子，节省开发维护成本

`

