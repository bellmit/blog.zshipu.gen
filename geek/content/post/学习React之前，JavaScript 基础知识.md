
---
title: 学习React之前，JavaScript 基础知识
author: 知识铺
date: 2021-01-25 22:11:56+08:00
tags: []
---
在深入了解 React 之前了解有关 JavaScript 和 Web 开发的所有信息。不幸的是， 我们生活在一个不完美的世界里， 所以在 React 之前对所有 JavaScript 进行大做笑只会让你流血。如果您已经拥有了一些 JavaScript 的经验，那么在 React 之前，您需要学习的只是用于开发 React 应用程序的 JavaScript 功能。关于JavaScript，在学习React之前，你应该对它感到自在：

*   [ES6 类](#es6-classes)
*   [新的变量声明 let/const](#declaring-variables-with-es6-let-and-const)
*   [箭头函数](#the-arrow-function)
*   [解构分配](#destructuring-assignment-for-arrays-and-objects)
*   [地图和过滤器](#map-and-filter)
*   [ES6 模块系统](#es6-module-system)

这是20%的JavaScript功能，你将使用80%的时间，所以在本教程中，我将帮助您学习他们所有。

## [](#exploring-create-react-app)<font _mstmutation="1" _msthash="289354" _msttexthash="38795289">探索创建React应用程序</font>

<font _mstmutation="1" _msthash="276809" _msttexthash="858278031">开始学习 React 的通常情况是运行包，它设置运行 React 所需的一切。然后，在过程完成后，打开将呈现我们整个应用程序中唯一的 React 类：</font>```create-react-app``````src/app.js```

 <code>import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;</code> 

如果您以前从未学习过 ES6，你会认为此类语句是 React 的一个功能。它实际上是 ES6 的新功能，这就是为什么正确学习 ES6 使您能够更好地了解 React 代码的原因。我们将从 ES6 课程开始。

## [](#es6-classes)<font _mstmutation="1" _msthash="290550" _msttexthash="4163939">ES6 类</font>

<font _mstmutation="1" _msthash="277953" _msttexthash="439772242">ES6 引入了类语法，其使用方式与 OO 语言（如 Java 或 Python）类似。ES6 中的基本类将看起来像：</font>

 <code>class Developer {
  constructor(name){
    this.name = name;
  }

  hello(){
    return 'Hello World! I am ' + this.name + ' and I am a web developer';
  }
}</code> 

```class```<font _mstmutation="1" _msthash="290316" _msttexthash="879162011">语法后跟一个标识符（或简单名称），可用于创建新对象。该方法始终在对象初始化中调用。传递到对象的任何参数都将传递到新对象中。例如：</font>```constructor```

 <code>var nathan = new Developer('Nathan');
nathan.hello(); // Hello World! I am Nathan and I am a web developer</code> 

<font _mstmutation="1" _msthash="290914" _msttexthash="347388080">类可以定义尽可能多的方法，因为需要，在这种情况下，我们有返回字符串的方法。</font>```hello```

### [](#class-inheritance)<font _mstmutation="1" _msthash="304954" _msttexthash="9228700">类继承</font>

<font _mstmutation="1" _msthash="291512" _msttexthash="259041822">类可以定义另一个类，从该类初始化的新对象将具有这两个类的所有方法。</font>```extends```

 <code>class ReactDeveloper extends Developer {
  installReact(){
    return 'installing React .. Done.';
  }
}

var nathan = new ReactDeveloper('Nathan');
nathan.hello(); // Hello World! I am Nathan and I am a web developer
nathan.installReact(); // installing React .. Done.</code> 

<font _mstmutation="1" _msthash="292110" _msttexthash="1351064442">另一个类通常称为_子类或__子类的_类，而正在扩展的类称为_父类或__超级类_。子类还可以_重写_父类中定义的方法，这意味着它将用定义的新方法替换方法定义。例如，让我们重写函数：</font>```extends``````hello```

 <code>class ReactDeveloper extends Developer {
  installReact(){
    return 'installing React .. Done.';
  }

  hello(){
    return 'Hello World! I am ' + this.name + ' and I am a REACT developer';
  }
}

var nathan = new ReactDeveloper('Nathan');
nathan.hello(); // Hello World! I am Nathan and I am a REACT developer</code> 

<font _mstmutation="1" _msthash="292708" _msttexthash="57617443">给你。类中的方法已被覆盖。</font>```hello``````Developer```

### [](#use-in-react)<font _mstmutation="1" _msthash="304005" _msttexthash="17284943">在React中使用</font>

<font _mstmutation="1" _msthash="290602" _msttexthash="1017041571">现在，我们了解 ES6 类和继承，我们可以理解 在 中定义的 React 类。这是一个 React 组件，但实际上只是一个正常的 ES6 类，它继承了从 React 包导入的 React 组件类的定义。</font>```src/app.js```

 <code>import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    return (
      <h1>Hello React!</h1>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="291200" _msttexthash="1467347739">这使我们能够使用方法，JSX，其他方法。所有这些定义都在类中。但是，正如我们稍后将看到的，类并不是定义 React 组件的唯一方法。如果不需要状态和其他生命周期方法，可以改为使用函数。</font>```render()``````this.state``````Component```

## [](#declaring-variables-with-es6-raw-let-endraw-and-raw-const-endraw-)<font _mstmutation="1" _msthash="304980" _msttexthash="8374158">使用 ES6 和</font>```let``````const```

<font _mstmutation="1" _msthash="291798" _msttexthash="2898498759">由于 JavaScript 关键字全局声明变量，因此在 ES6 中引入了两个新的变量声明来解决此问题，即 和 。它们都是一样的，它们用于声明变量。区别在于不能在声明后更改其值，而可以。这两个声明都是本地的，这意味着如果在函数范围内声明，则不能在函数之外调用它。</font>```var``````let``````const``````const``````let``````let```

 <code>const name = "David";
let age = 28;
var occupation = "Software Engineer";</code> 

### [](#which-one-to-use)<font _mstmutation="1" _msthash="306189" _msttexthash="23160241">使用哪一个？</font>

<font _mstmutation="1" _msthash="292695" _msttexthash="1583964473">经验法则是默认使用声明变量。稍后，当您撰写应用程序时，您将意识到需要更改的价值。这是您应该重构为 的时间。希望它能让你习惯新的关键字，并且你会开始识别应用程序中需要使用或 的模式。</font>```const``````const``````const``````let``````const``````let```

### [](#when-do-we-use-it-in-react)<font _mstmutation="1" _msthash="306813" _msttexthash="67123303">我们什么时候在React中使用它？</font>

<font _mstmutation="1" _msthash="290589" _msttexthash="101511280">每次我们需要变量。请考虑以下示例：</font>

 <code>import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    const greeting = 'Welcome to React';
    return (
      <h1>{greeting}</h1>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="291187" _msttexthash="259714468">由于问候语在整个应用程序生命周期中不会改变，因此我们使用此处定义它。</font>```const```

## [](#the-arrow-function)<font _mstmutation="1" _msthash="304967" _msttexthash="12023492">箭头功能</font>

<font _mstmutation="1" _msthash="291785" _msttexthash="876119335">Arrow 函数是一种新的 ES6 功能，在现代代码库中几乎被广泛使用，因为它使代码保持简洁和可读性。此功能允许我们使用较短的语法编写函数</font>

 <code>// regular function
const testFunction = function() {
  // content..
}

// arrow function
const testFunction = () => {
  // content..
}</code> 

如果您是经验丰富的 JS 开发人员，则从常规函数语法移动到箭头语法可能首先会让人不舒服。当我学习箭头函数时，我使用这个简单的 2 个步骤来重写我的函数：

1.  删除函数关键字
2.  <font _mstmutation="1" _msthash="463333" _msttexthash="34433828">添加脂肪箭头符号后</font>```=>``````()```

<font _mstmutation="1" _msthash="292981" _msttexthash="176379190">括号仍用于传递参数，如果只有一个参数，可以省略括号。</font>

  <code>const testFunction = (firstName, lastName) => {
  return firstName+'  '+lastName;
}

const singleParam = firstName => {
  return firstName;
}</code> 

### [](#implicit-return)<font _mstmutation="1" _msthash="304603" _msttexthash="13237224">隐式返回</font>

<font _mstmutation="1" _msthash="291174" _msttexthash="222532830">如果您的箭头函数只有一行，则无需使用关键字和大括号即可返回值</font>```return``````{}```

 <code>const testFunction = () => 'hello there.';
testFunction();</code> 

### [](#use-in-react)<font _mstmutation="1" _msthash="305539" _msttexthash="17284943">在React中使用</font>

<font _mstmutation="1" _msthash="292071" _msttexthash="239837936">创建 React 组件的另一种方法是使用箭头函数。React采取箭头功能：</font>

 <code>const HelloWorld = (props) => {
  return <h1>{props.hello}</h1>; }</code> 

<font _mstmutation="1" _msthash="292669" _msttexthash="22925058">相当于 ES6 类组件</font>

 <code>class HelloWorld extends Component {
  render() {
    return (
      <h1>{props.hello}</h1>;
    );
  }
}</code> 

在 React 应用程序中使用箭头函数会使代码更加简洁。但它也会从组件中删除状态的使用。这种类型的组件称为无_状态功能组件_。您可以在许多 React 教程中找到该名称。

## [](#destructuring-assignment-for-arrays-and-objects)<font _mstmutation="1" _msthash="307138" _msttexthash="42338439">数组和对象的析构分配</font>

<font _mstmutation="1" _msthash="291161" _msttexthash="647886616">ES6 中引入的最有用的新语法之一，解构赋值只是复制对象或数组的一部分，并将它们放入命名变量中。一个快速示例：</font>

 <code>const developer = {
  firstName: 'Nathan',
  lastName: 'Sebhastian',
  developer: true,
  age: 25,
}

//destructure developer object
const { firstName, lastName } = developer;
console.log(firstName); // returns 'Nathan'
console.log(lastName); // returns 'Sebhastian'
console.log(developer); // returns the object</code> 

<font _mstmutation="1" _msthash="291759" _msttexthash="580211008">如您所看到的，我们将名字和姓氏从对象分配到新的变量 和 中。现在，如果要放入名为 ？ 的新变量，怎么办？</font>```developer``````firstName``````lastName``````firstName``````name```

 <code>const { firstName:name } = developer;
console.log(name); // returns 'Nathan'</code> 

<font _mstmutation="1" _msthash="292357" _msttexthash="171502474">解构也适用于数组，只有它使用索引而不是对象键：</font>

 <code>const numbers = [1,2,3,4,5];
const [one, two] = numbers; // one = 1, two = 2</code> 

<font _mstmutation="1" _msthash="292955" _msttexthash="140179845">您可以通过 使用 传递来从析构中跳过某些索引：</font>```,```

 <code>const [one, two, , four] = numbers; // one = 1, two = 2, four = 4</code> 

### [](#use-in-react)<font _mstmutation="1" _msthash="307398" _msttexthash="17284943">在React中使用</font>

<font _mstmutation="1" _msthash="293852" _msttexthash="74370465">主要用于方法的析构，例如：</font>```state```

 <code>reactFunction = () => {
  const { name, email } = this.state;
};</code> 

<font _mstmutation="1" _msthash="291746" _msttexthash="155779156">或在功能无状态组件中，请考虑上一章中的示例：</font>

 <code>const HelloWorld = (props) => {
  return <h1>{props.hello}</h1>; }</code> 

<font _mstmutation="1" _msthash="292344" _msttexthash="52835159">我们可以立即销毁参数：</font>

 <code>const HelloWorld = ({ hello }) => {
  return <h1>{hello}</h1>; }</code> 

<font _mstmutation="1" _msthash="292942" _msttexthash="67426411">解构数组也用于 React 的挂钩：</font>```useState```

 <code>const [user, setUser] = useState('');</code> 

## [](#map-and-filter)<font _mstmutation="1" _msthash="307112" _msttexthash="19174662">地图和过滤器</font>

<font _mstmutation="1" _msthash="293839" _msttexthash="906049547">尽管本教程重点介绍 ES6，但需要提及 JavaScript 数组和方法，因为它们可能是构建 React 应用程序时使用最多的 ES5 功能之一。特别是在处理数据方面。</font>```map``````filter```

<font _mstmutation="1" _msthash="294138" _msttexthash="310309337">这两种方法在处理数据时使用得多。例如，假设从 API 结果提取返回 JSON 数据数组：</font>

 <code>const users = [
  { name: 'Nathan', age: 25 },
  { name: 'Jack', age: 30 },
  { name: 'Joe', age: 28 },
];</code> 

<font _mstmutation="1" _msthash="292032" _msttexthash="177243729">然后，我们可以在 React 中呈现项目列表，如下所示：</font>

 <code>import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    const users = [
      { name: 'Nathan', age: 25 },
      { name: 'Jack', age: 30 },
      { name: 'Joe', age: 28 },
    ];

    return (
      <ul>
        {users
          .map(user => <li>{user.name}</li>)
        }
      </ul>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="292630" _msttexthash="62277540">我们还可以筛选渲染中的数据。</font>

 <code><ul>
  {users
    .filter(user => user.age > 26)
    .map(user => <li>{user.name}</li>)
  }
</ul></code> 

## [](#es6-module-system)<font _mstmutation="1" _msthash="306787" _msttexthash="17230707">ES6 模块系统</font>

<font _mstmutation="1" _msthash="293527" _msttexthash="422581939">ES6 模块系统使 JavaScript 能够导入和导出文件。让我们再次查看代码，以便对此进行解释。</font>```src/app.js```

 <code>import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;</code> 

<font _mstmutation="1" _msthash="294125" _msttexthash="102565905">在第一行代码中，我们看到导入语句：</font>

 <code>import React, { Component } from 'react';</code> 

<font _mstmutation="1" _msthash="292019" _msttexthash="53115907">最后一行我们看到语句：</font>```export default```

 <code>export default App;</code> 

为了理解这些语句，我们先讨论一下模块语法。

<font _mstmutation="1" _msthash="292916" _msttexthash="630586567">模块只是使用 关键字导出一个或多个值（可以是对象、函数或变量）的 JavaScript 文件。首先，创建一个在目录中命名的新文件</font>```export``````util.js``````src```

 <code>touch util.js</code> 

<font _mstmutation="1" _msthash="293514" _msttexthash="96771870">然后在它里面写一个函数。这是默认**导出**</font>

 <code>export default function times(x) {
  return x * x;
}</code> 

<font _mstmutation="1" _msthash="294112" _msttexthash="20107243">或多个**命名导出**</font>

 <code>export function times(x) {
  return x * x;
}

export function plusTwo(number) {
  return number + 2;
}</code> 

<font _mstmutation="1" _msthash="294710" _msttexthash="38654252">然后，我们可以导入它</font>```src/App.js```

 <code>import { times, plusTwo } from './util.js';

console.log(times(2));
console.log(plusTwo(3));</code> 

<font _mstmutation="1" _msthash="292604" _msttexthash="575004885">每个模块可以有多个命名导出，但只能有一个默认导出。无需使用大括号和相应的导出函数名称即可导入默认导出：</font>

 <code>// in util.js
export default function times(x) {
  return x * x;
}

// in app.js
import k from './util.js';

console.log(k(4)); // returns 16</code> 

<font _mstmutation="1" _msthash="293202" _msttexthash="655404659">但对于命名导出，必须使用大括号和确切名称进行导入。或者，导入可以使用别名来避免对两个不同的导入具有相同的名称：</font>

 <code>// in util.js
export function times(x) {
  return x * x;
}

export function plusTwo(number) {
  return number + 2;
}

// in app.js
import { times as multiplication, plusTwo as plus2 } from './util.js';</code> 

<font _mstmutation="1" _msthash="293800" _msttexthash="52359268">从绝对名称导入，如：</font>

 <code>import React from 'react';</code> 

<font _mstmutation="1" _msthash="294398" _msttexthash="447478317">将使 JavaScript 检查相应的包名称。因此，如果要导入本地文件，不要忘记使用正确的路径。</font>```node_modules```

### [](#use-in-react)<font _mstmutation="1" _msthash="308594" _msttexthash="17284943">在React中使用</font>

<font _mstmutation="1" _msthash="294996" _msttexthash="504624289">显然，我们在文件中看到了这一点，然后在呈现导出组件的文件中看到了这一点。现在让我们忽略服务工部分。</font>```src/App.js``````index.js``````App```

 <code>//index.js file

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();</code> 

<font _mstmutation="1" _msthash="305305" _msttexthash="1900842112">请注意如何从目录导入应用，并且已省略扩展名。只有在导入 JavaScript 文件时，我们才能删除文件扩展名，但我们必须将它包括在其他文件（如 ） 中。我们还导入另一个节点模块 ，这使我们能够将 React 组件呈现到 HTML 元素中。</font>```./App``````.js``````.css``````react-dom```

对于 PWA，它是使 React 应用程序脱机工作的功能，但由于默认情况下禁用它，因此无需在开始时学习它。在您有足够的信心构建 React 用户界面后，最好学习 PWA。

## [](#conclusion)<font _mstmutation="1" _msthash="320008" _msttexthash="6674577">结论</font>

React 的厉害之处是，它不会像其他 Web 框架一样在 JavaScript 的上面添加任何外国抽象层。这就是为什么 React 在 JS 开发人员中变得非常流行。它只是使用最好的JavaScript，使构建用户界面更容易和可维护。React 应用程序中的 JavaScript 确实比 React specfix 语法更多，因此，一旦您更好地了解 JavaScript（尤其是 ES6），就可以自信地编写 React 应用程序。但这并不意味着您必须掌握有关 JavaScript 的一切才能开始编写 React 应用程序。现在就去写一个，随着机会的来，你将成为一个更好的开发人员。

