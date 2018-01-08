视图是数据的映射（单向数据流）
React 是一个视图层的框架，所谓视图层就是我们在网页上能看到的部分。在传统的方式中，我们通过编写HTML代码来设计网页的结构，通过 JavaScript 以及 getElementById 等 api 来获取某个节点，通过节点的 innerHTML，innerText，appendChild 等属性或者方法（或者你也可能用JQuery）来更新视图。

在 React 时代，你除了需要自己考虑网页的结构和CSS样式外，视图的更新 React 统统帮你搞定。

那么，用了 React 我们如何来更新视图呢，先看下面这个张图：



在 React 中视图是数据的映射，你想要视图发生变化，那你只要改变数据就好了，就是这么简单。

举个简单的例子，你打算在你的页面上展示用户的名片，名片上有照片、姓名、年龄、地址等基本信息，如下图所示：



这个名片，作为视图的一部分，在 React 中是由某个用户的数据映射而来的，可能长得像这样：

{
    photo: "my-photo.jpeg",
    name: "sarike",
    age: 18,
    address: "北京"
}
如果你希望网页的浏览者，可以切换查看不同用户的名片，你要做的只是用下一个用户的数据替换一下当前的数据就可以了。至于新的数据是如何替换掉页面上的旧数据的，就无需关心了，React 会以最高效的方式帮你完成。

这也就是所谓的单向数据流，在这种开发方式下，会让你更新视图的逻辑非常清晰、简单，哪怕你的前端交互很复杂，也不至于让你的代码那么容易变成一坨。

是不是很爽？

面向组件编程
上一部分说的 React 中更新视图只需要更新数据就可以了，如果你觉得也就一般般吧，那下面要说的一定爽到爆。

先说一下什么是组件，顾名思义，组件就是用来组合成更高级东西的物件。打个比方，比如一辆汽车，汽车中的各种螺丝、铁块等零件就可以看作是一个个组件，这些小的组件我们还可以继续组合，比如组合成发动机、轮胎、车架等有特定功能的组件，然后这些组件又可以继续组合成一辆完整的汽车。

对应到我们的前端开发中，HTML中的各种元素（如：div，table，input，select等）就是一个个最基本的组件，你可以把他们继续组合，组合成第一部分说的名片，或者一个填写用户信息的表单，展示所用用户的一个列表等有特定业务功能的组件，各种各样的业务组件最终组合成一个完整的前端页面。

组件最大的特点就是可以重复利用，比如说用户名片这个组件，你可以放到个人信息页面，也可以放到文章详情页面来展示作者信息，制作完成，到处利用。

言归正传，那在使用 React 是，是如何面向组件编程的呢，现在你可以这样来理解，React 提供了一种可以创造新的 HTML 标签的能力。

例如第一部分讲的用户名片的例子，通过 React 你可以制作这样一个组件：

<Card name="sarike" age="18" address="北京" />
而且更重要的是，你可以以如此简单的方式在你应用的任何位置重复利用。

你说，酷不酷，爽不爽？！！

至此以后，你在开发一个前端页面时，你需要做的就是将页面拆分成各种组件，然后把它们组合起来就好了。

在此想跟大家分享一点小经验，这也关系到你最终能不能将 React 用得很溜。就是：在前端开发过程中，要善于观察和抽象。尤其是在项目前期，不要着急写代码，一定观察项目的原型图或者设计稿，想想哪些部分是可以拆分成可以复用的公共组件的。这样做能让你后面的工作，事半功倍。

在后面的文章中你将更深入地体会到这一点，同时你也会体会到 React 的组件化开发，到底是多么多么的爽！！


React 第一印象
废话不多说，先看一段代码：

class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

ReactDOM.render(<HelloMessage name="John" />, mountNode);
这是从 React 官网首页粘贴过来的一段示例代码，简单解释一下，这段代码实现了一个名为 HelloMessage 的组件，它接收一个 name 属性，可以在页面上展示出 Hello xxx。ReactDOM.render 是用来将某个组件渲染到页面的某个 DOM 节点上。

在之后的文章中，我们会详细讲解如何创建 React 组件以及如何开发一个完整的 React 项目。现在，我更想跟大家探讨的是，你看了上述这段代码，算是对 React 有了第一印象，内心是怎样的感受？

我相信，很多人第一次看到这样的代码时的感受都是：“我擦，这是什么玩意儿，HTML怎么都写到JavaScript代码里去了，展示与业务逻辑分离，这都不懂？”，说实话，这就是我当时真实的内心感受。很幸运我坚持了下去，并一直用到现在，现在我对 React 的感受是：“我擦，好爽，好牛逼”。

刚开始有这种想法很好理解，好多人像我一样被“展示要与业务逻辑分离”这句话洗脑太久了，其实，这句话真正发挥价值的时候，是在 MVC 开发模式出现之前，那时候 web 程序逻辑很简单，可能页面开始处是连接数据库，查询数据，接在下面就是 HTML 代码来展示查询结果了。如果你了解一点 PHP，在 PHP 文件的开始处有个 <?php 结尾处可能有个 ?>，这就是那个年代用来分隔 PHP 代码和 HTML 代码的。但是随着 web 程序逻辑越来越复杂，业务逻辑代码跟 HTML 代码混到一起就变得越来越难以维护，所以就有了 MVC 开发模式。

并不是说现在“展示要与业务逻辑分离”这句话已经不适用于现在的 web开发，我想说的是，我们看问题，要回归问题的本质，我们要不要接受 React 的这种写法，判断依据应该是基于 React 的这种写法有没有让我们的前端代码变得更清晰、易维护性更强，而不是 JavaScript 中是不是写了类似于 HTML 语法的东西，千万不要为了分离而分离。

其实只是给JavaScript加了点糖 - JSX
上面这种在 JavaScript 中写类似 HMTL 代码的语法被称为 JSX。你可以理解为扩展版的 JavaScript。显然，这种语法在浏览器环境中是不能执行的，所以在代码加载到页面中之前，我们需要通过工具将它转译成标准的 JavaScript 语法，就像我们现在为什么可以用 ES6 的语法一样，尽管目前浏览器对它支持得还不好。例如下面这两段代码，实际上是等价的。

JSX 语法：

const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
由上面代码转译而来的标准 JavaScript 语法：

const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
是不是感觉 JSX 语法更直观，写起来更简洁？所以说 JSX 实际上是 React.createElement(component, props, ...children) 的语法糖。

如果你熟悉 HTML，那么 JSX 对于你来说是没有任何压力的，因为 HTML 中的所有标签，在 JSX 中都是支持的，基本上没有学习成本，只有如下几点略微的不同：

class 属性变为 className
tabindex 属性变为 tabIndex
for 属性变为 htmlFor
textarea 的值通过需要通过 value 属性来指定
style 属性的值接收一个对象，css 的属性变为驼峰写法，如：backgroundColor。
在上一篇中，我们有提到组件，实际上，我们可以把在 JSX 中写的 HTML 标签看作是 React 内部已经实现了的基础组件。在下一篇中我将详细为大家介绍如何利用这些基础组件来创造一个新的组件，也就是上一篇提到的 React 所提供的创建一个新的 HTML 标签的能力。


内容摘要
定义组件两种方式：类继承组件、函数式组件。
类继承组件有更丰富的特性，函数式组件书写更简洁，执行效率更高。
组件名称首字母要大写。
属性是一个组件的外部输入。
属性值可以通过 {} 设置任意的 JS 表达式。
属性是只读的。
属性可以设置默认值。
属性可以设置类型，开发阶段 React 会对属性进行类型检查。
为组件所有属性设置类型检查是个好习惯，有助于协作开发。
通过内容摘要可以让你快速了解本文内容是否对你有用，从而决定是否继续阅读，节省你的时间也是一件很有意义的事情。

定义组件的几种姿势
下面介绍一下在 React 中定义组件的几种方式。

1. 类继承
有过 Java 等面向对象开发经验的同学一定很容易接受这种方式。ES6 为 JavaScript 增加了类和类继承的特性。子类会继承父类的“基因”（成员方法、属性），如果父类是一个组件，那子类自然而然也是一个组件。

React 提供了 Component 和 PureComponent 两个父类，他们之间有一点点区别，我们在之后的文章中会详细介绍，现在你可以将他们同等看待，暂且无须理会。

通过继承自 React 提供的组件基类，我们可以这样来创建一个组件：

import React, {Component} from 'react';

class HelloMessage extends Component {
    render() {
        return <div>Hello world.</div>;
    }
}
通过类继承的方式创建一个组件，就是这么简单，只要继承 Component 基类并实现 render 方法即可。然后就可以把 HelloMessage 当成一个新的“HTML 标签”来用了，如下你可以把它渲染到页面上：

ReactDOM.render(<HelloMessage />, document.querySelector('#root'));
你也可以用它来装配其它组件，如：

import React, {Component} from 'react';

class HelloMessageList extends React.Component {
    render() {
        return (
            <div>
                <HelloMessage />
                <HelloMessage />
                <HelloMessage />
            </div>
        )
    }
}
当然，例子没有任何实际意义，只是为了演示组件的定义及其用法。

演示代码：https://codepen.io/Sarike/pen...点击预览

2. 函数式组件
顾名思义，函数式组件，就是以函数的形式来定义一个组件，如下所示：

import React from 'react';

function HelloMessage() {
    return <div>Hello world.</div>;
}

// 或者：

const HelloMessage = () => <div>Hello world.</div>;
实际上就是只实现了类继承方式中的 render 方法。

示例代码：https://codepen.io/Sarike/pen...点击预览

类继承 vs 函数式组件
这两种定义组件的方式，在实际的开发中都经常会被用到，对大部分人来说类继承的方式用得频率会更高一些。

类继承的方式，相较于函数式组件，虽然写起来略繁琐，但是它拥有更多的特性：

内部状态：state
生命周期函数
函数式组件虽然没有 state 和生命周期函数等特性，但是它有更简洁的书写方式，另外还有更好的性能，不用处理一些复杂的特性，执行效率当然高了。

现在你可以无需关心 state 和生命周期函数的具体作用，下一篇文章我会详细讲解，等你看完下一篇文章之后，至于选择哪种方式的问题就很好解决了。在开发一个组件的时候，我是这样来做的：当我一开始就知道这个组件会用到 state 或者生命周期函数时，毫无疑问直接使用类继承的方式；如果一开始用不到这些特性也不确定未来会不会用到，那我就先用函数式组件，如果随着业务的演进，组件需要应用这些特性的时候，我会再把它重构成类继承的方式。这个重构非常简单，只需要将原来的函数变成组件类的 render 方法即可。

另外，还有一点需要注意，不管那种方式，组件的名称首字母必须为大写。严格来说，是 JSX 要求用户自定义的组件名首字母必须为大写，如果是小写字母开头，那么 React 会将其当成内置的组件直接将其渲染成一个 html 标签，从而不会正确渲染用户自定义的组件。

如果你非要将组件名称以小写字母开头，那你在以 JSX 语法使用之前也必须将其赋值为一个大写字母开头的变量，如下所示：

function helloMessage() {
    return <div>Hello world.</div>
}

const HelloMessage = helloMessage;

ReactDOM.render(<HelloMessage />, mountNode);
但这有事何必呢，纯粹是没事儿找事儿，大家在实际项目开发时，直接将组件名以大写字母开头即可。

属性
上面说完了在 React 中两种定义组件的方式。在上面的例子中，我们定义的组件都是静态的，然而在实际的开发中，视图层组件往往会进行频繁更新，或者需要从后端 API 获取动态数据在组件中展示。这就需要组件拥有接收外部输入的能力。

属性是组件的输入
在第二篇文章 《新型前端开发方式》 中有说到 “视图是数据的映射”，那么其中说的数据指的就是属性。

如果把组件理解为一个函数，那么属性就是这个函数的参数，函数的返回值就是呈现到页面上的视图。而且通过上面部分的学习，在 React 中组件确实可以以函数的形式来定义，而且函数的参数就是一个包含当前组件接收到的所有属性的对象。

如下所示带有属性 name 的组件定义：

import React, {Component} from 'react';

class HelloMessage extends Component {
    render() {
        return <div>Hello {this.props.name}.</div>;
    }
}
函数式：

import React from 'react';

function HelloMessage(props) {
    return <div>Hello {props.name}.</div>;
}

// 或者：

const HelloMessage = props => <div>Hello {props.name}.</div>;
属性的传递也跟 HTML 一样（在本文的最后一部分会有各种类型属性的详细介绍），如下所示：

import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class HelloMessageList extends Component {
    render() {
        return (
            <div>
                <HelloMessage name="Lucy" />
                <HelloMessage name="Tom" />
                <HelloMessage name="Jack" />
            </div>
        )
    }
}

ReactDOM.render(<HelloMessageList />, document.querySelector('#root'));
这样页面上会展示出：

Hello Lucy.
Hello Tom.
Hello Jack.
示例代码：https://codepen.io/Sarike/pen...点击预览

属性必须为只读的
属性必须为只读的，这一点非常重要，请严格遵守。对应到上面说到的，如果把组件理解为一个函数，那么这个函数必须为一个纯函数（Pure function），在纯函数中不能修改其参数，确定的输入必须有确定的输出。

虽然有些时候，你修改了组件的属性，貌似也能正常工作。没错，因为 JavaScript 语言特性的原因，没人能阻止你这么做。但是请先相信我，严格遵守这条规则不仅能让你少踩很多坑，而且能让你的应用稳定性更强、维护性更强。如果你直接修改组件的属性，React 并不会感知到此修改，从而不会重新渲染组件，就导致了当前组件的视图展示与数据不一致，但这个被修改的属性会随着下一次组件的渲染被生效到视图上，而且这次渲染的时机是不确定的，不难想象，如果一个规模较大的项目里充满了这种不确定性是多么痛苦的一件事情。总之，如果你随意修改组件的属性，会很容易让你的应用充满许多难以排查的 BUG。

默认属性
通常情况下，我们需要为组件的属性设为默认值。就像 HTML 标签的属性也有默认值一样，例如 form 标签的 method 属性默认值是 GET，input 标签的 type 属性默认值是 text 一样。

还是上面 HelloMessage 组件，如果需求是当不传入 name 属性时，默认展示 Hello World.，也就是说 name 属性的默认值是 World。

一种很容易想到的做法：

<div>Hello {this.props.name || 'World'}.</div>
这样确实可以解决当前这个需求，但是属性可能还会是个 Object，也可能是个函数，你当然可以先判断下这个属性是否为 undefined 然后决定是否使用默认值，但是这样会让代码显得很不优雅，而且也会增加很多繁琐的判断逻辑。

因此，React 提供了相应的机制可以设置组件属性的默认值，如下所示，你需要通过组件的静态字段 defaultProps 来设置组件属性的默认值。如下所示：

import React, {Component} from 'react';

class HelloMessage extends Component {
    render() {
        return <div>Hello {this.props.name}.</div>;
    }
}
HelloMessage.defaultProps = {
    name: 'World'
}
这样就可以了，<HelloMessage /> 这样不为组件设置任何属性，那么它就会在页面上展示Hello World.。

示例代码：https://codepen.io/Sarike/pen...点击预览

属性的类型及校验
在开发较复杂的前端应用时，我们经常会遇到许多因为类型检查导致的问题，例如上面的 HelloMessage 组件，我期望其 name 属性只能是字符串类型的，你要是给我一个 Object，我是没法正确展示的。为了在开发过程中尽快的发现这类问题，React 为组件添加了类型检查的机制，你需要给组件设置静态字段 propTypes 来设置组件各个属性的类型检查器。

import React, {Component} from 'react';
import PropTypes from 'prop-types';

class HelloMessage extends Component {
    render() {
        return <div>Hello {this.props.name}.</div>;
    }
}
HelloMessage.defaultProps = {
    name: 'World'
}
HelloMessage.propTypes = {
    name: PropTypes.string
}
这样在开发过程中 React 就能校验组件接收到的属性值是否符合指定的类型，如果校验不通过，将会抛出警告。React 只会在开发模式下进行属性类型检查，当代码进行生产发布后，为了减少额外的性能开销，类型检查将会被略过。

其实，为每一个组件编写完善的属性类型是一个非常好的习惯，这不仅能及时发现问题，更重要的是配合几句简单额注释，这将成为该组件一份非常好的文档，一个完善的组件应该具有良好的封装性和易复用性，在一个协作开发的项目中，其他开发者需要引用你开发的组件时，只需要看一下组件的属性列表，大致就可以了解如何来使用这个组件，省去了很多不必要的沟通。

下面是 React 提供的可用的数据类型检查器。

PropTypes.array
PropTypes.bool
PropTypes.func
PropTypes.number
PropTypes.object
PropTypes.string
PropTypes.symbol
PropTypes.element 元素，其实就是 JSX 表达式，上一篇文章有说过 JSX 是 React.createElement 的语法糖，一个 JSX 表达式实际上会生成一个 JS 对象，在 React 中称之为元素（Element）。
PropTypes.node 所有可以被渲染的数据类型，包括：数值, 字符串, 元素或者这些类型的数组。
PropTypes.instanceOf(Message) 某个类的实例
PropTypes.oneOf(['News', 'Photos']) 枚举，属性值必须为其中的某一个值。
PropTypes.oneOfType([PropTypes.string, PropTypes.number]) 类型枚举，属性必须为其中某一个类型。
PropTypes.arrayOf(PropTypes.number) 属性为一个数组，且数组中的元素必须符合指定类型。
PropTypes.objectOf(PropTypes.number) 属性为一个对象，且对象中的各个字段的值必须符合指定类型。
PropTypes.any 任何类型
如果你想指定某些属性为必需属性，你可以链式调动其 isRequired 来标识某个属性对于当前组件来说是必需的。如果在使用组件时未指定则会抛出警告提醒。

另外你还可以通过一个函数自定义属性验证器，如果验证不通过你需要返回一个 Error 实例，如下所示：

function(props, propName, componentName) {
  if (!/matchme/.test(props[propName])) {
    return new Error(
      'Invalid prop `' + propName + '` supplied to' +
      ' `' + componentName + '`. Validation failed.'
    );
  }
}
设置组件的属性值
上面咱们了解到组件的属性有很多种类型，下面说一下各种类型的属性是如何传递给组件的。其实很简单，属性的值可以用一对大括号 { } 来包围，其中可以指定任意的 JavaScript 表达式。如下所示：

return (
    <User
        name="Tom"                            // 字符串
        age={18}                              // 数值
        isActivated={true}                    // 布尔值
        interests={['basketball', 'music']}   // 数组
        address={{ city: 'Beijing', road: 'BeiWuHuan' }} // 对象
    />
)
展开操作符
你也可以用展开操作符 ... 将一个对象的所有字段展开，依次作为属性传递给组件，上面的代码等价于：

const userInfo = {
    name: 'Tom',
    age: 18,
    isActivated: true,
    interests: ['basketball', 'music'],
    address: { city: 'Beijing', road: 'BeiWuHuan' }
}
return <User {...userInfo} />
值为 true 的属性的简写
如果是属性类型为布尔值，且当前属性值为 true 可以只写属性名，如下所示：

<input
    disabled     // 禁用该输入框
    type="text"
/>
children 属性
用户自定义的组件内可以通过 this.props.children 来获取一个特殊的属性。该属性与其它属性的区别就是传递方式不同。

children 属性的值是指一对闭合的 JSX 标签中间的内容，如下所示：

<UserList>
    <User name="Tom" />
    <User name="Lucy" />
</UserList>
那么在 UserList 内部可以通过 this.props.children 来获取下面这个 JSX 片段：

<User name="Tom" />
<User name="Lucy" />
该示例中，获取到的实际上是一个包含两个 User 元素对象的数组。

