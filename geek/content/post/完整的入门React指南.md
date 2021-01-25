
---
title: 完整的入门React指南
author: 知识铺
date: 2021-01-25 22:35:34+08:00
tags: [reactjs]
---
## [](#what-is-react)<font _mstmutation="1" _msthash="289055" _msttexthash="13230529">什么是React</font>

React 是 Facebook 开发团队在 2013 年构建的 JavaScript 库，用于使用户界面更加模块化（或可重用）且更易于维护。根据 React 的网站，它用于"构建管理自身状态的封装组件，然后组合它们以生成复杂的 UIs"。

我要在这篇文章中使用很多 Facebook 的例子， 因为他们写 React 摆在首位。

还记得 Facebook 从喜欢转向React吗？现在，您可以用一颗心、笑脸或喜欢的帖子来回应，而不是仅仅喜欢帖子。如果这些React主要是在HTML中做出，那么改变所有这些喜欢的React并确保它们有效将是一项巨大的工作。

这就是 React 的用武之所——我们在第一天就对开发人员印象深刻，而不是实现对开发人员印象深刻的"关注点分离"，而是在 React 中采用不同的体系结构，它基于组件结构增加模块化，而不是分离不同的编程语言。

> 今天，我们将将 CSS 分开，但如果您需要，甚至可以使该组件特定于该组件。

### [](#react-vs-vanilla-javascript)<font _mstmutation="1" _msthash="291122" _msttexthash="16953508">React与香草 Javascript</font>

当我们谈论"香草"JavaScript时，我们通常谈论的是编写不使用其他库（如JQuery、React、Angular或Vue）的JavaScript代码。如果你想阅读更多关于这些和什么是框架，我有一个帖子[所有关于](https://zshipu.com/t?url=https://welearncode.com/web-framework-intro)Web框架。

## [](#a-couple-quick-notes-before-we-begin)<font _mstmutation="1" _msthash="303745" _msttexthash="40253434">开始之前几个快速笔记</font>

*   <font _mstmutation="1" _msthash="462358" _msttexthash="396892158">若要使本教程更加简洁一点，某些代码示例在它们之前或之后具有，这意味着省略了某些代码。</font>```...```
*   <font _mstmutation="1" _msthash="462735" _msttexthash="536657758">我在某些地方使用 Git diffs 来显示将更改的代码行，因此，如果您复制和粘贴，则需要删除行的开头。</font>```+```
*   我有完整的 CodePens 与每个部分的完成版本 - 所以您可以使用这些追赶。
*   更高级的概念，不是必要的教程是块报价，这些大多只是事实，我认为是有趣的。

## [](#set-up)<font _mstmutation="1" _msthash="304369" _msttexthash="5481814">建立</font>

如果要创建生产 React 应用程序，您将需要使用生成工具（如 Webpack）来捆绑代码，因为 React 会使用一些在浏览器中默认不起作用的模式。[创建React](https://zshipu.com/t?url=https://github.com/facebook/create-react-app)应用程序对于这些目的非常有帮助，因为它会为你执行大部分配置。

<font _mstmutation="1" _msthash="291512" _msttexthash="1604911919">现在，由于我们希望快速启动和运行，以便编写实际的 React 代码，我们将使用 React CDN，它仅用于开发目的。我们还将使用 Babel CDN，以便可以使用一些非标准的 JavaScript 功能（我们稍后将讨论更多）。</font>

 <code><script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.25.0/babel.min.js"></script></code> 

我还做了一[个代用模板](https://zshipu.com/t?url=https://codepen.io/aspittel/pen/gdrexE)，你可以使用！

在一个完整的 React 项目中，我将我的组件拆分成不同的文件，但出于学习目的，我们将现在将 JavaScript 合并到一个文件中。

## [](#components)<font _mstmutation="1" _msthash="306241" _msttexthash="5055388">组件</font>

对于本教程，我们将建立一个Facebook状态小部件，因为Facebook写了React摆在首位。

<font _mstmutation="1" _msthash="290602" _msttexthash="3852120311">想想小部件在 Facebook 上显示多少个位置——你可以喜欢状态、链接帖子、视频帖子或图片。甚至一页！每次 Facebook 调整类似功能时， 他们都不想在所有这些地方这样做。所以，这就是组件的用向。网页的所有可重用部分都抽象为一个组件，可以一遍又一次地使用，我们只需在一个地方更改代码就可以更新它。</font>```like```

让我们看看 Facebook 状态的图片，并分解其中的不同组件。

[![A Facebook status](https://res.cloudinary.com/practicaldev/image/fetch/s--D_FmFTGG--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/s218x9fpea5y9cwvhcx3.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--D_FmFTGG--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/s218x9fpea5y9cwvhcx3.png)

状态本身将是一个组件 - 在 Facebook 时间线中有很多状态，因此我们当然希望能够重用状态组件。

<font _mstmutation="1" _msthash="291798" _msttexthash="724376367">在该组件中，_我们将在父组件中_具有子组件或组件。这些组件也是可重用的，因此我们可以让像按钮组件一样是组件和组件的子组件。</font>```PhotoStatus``````LinkStatus```

也许我们的子组件看起来像这样：

[![A diagram of breaking down react components](https://res.cloudinary.com/practicaldev/image/fetch/s--6ca1Fa5p--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/1s4oddo313hnqs7qosyv.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--6ca1Fa5p--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/1s4oddo313hnqs7qosyv.png)

<font _mstmutation="1" _msthash="292695" _msttexthash="685747855">我们甚至可以在子组件内有子组件！因此，喜欢、评论和共享的组可能是它自己的组件，组件用于喜欢其中的评论和共享！</font>```ActionBar```

[![A diagram of subcomponents within subcomponents](https://res.cloudinary.com/practicaldev/image/fetch/s--uiNFbLaT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/buukhx6ztlizgj7z95je.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--uiNFbLaT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/buukhx6ztlizgj7z95je.png)

有许多方法可以分解这些组件和子组件，具体取决于您将在应用程序中重用该功能的地点。

## [](#getting-started)<font _mstmutation="1" _msthash="304343" _msttexthash="4603768">开始</font>

我想开始本教程与React"你好世界" - 这是传统毕竟！然后，我们将转到稍微复杂的状态示例。

<font _mstmutation="1" _msthash="291486" _msttexthash="814113586">在我们的 HTML 文件中，让我们只添加一个元素 -- 一个包含 ID 的元素。按照惯例，您通常会看到 div 的 ID"root"，因为它将成为我们 React 应用程序的根。</font>```div```

 <code><div id="root"></div></code> 

<font _mstmutation="1" _msthash="292084" _msttexthash="1018679116">如果要在 CodePen 模板中[编写代码，](https://zshipu.com/t?url=https://codepen.io/aspittel/pen/gdrexE?editors=0010)可以直接在节中编写此 JavaScript。如果改为在计算机上编写此内容，则必须添加具有 类型的 脚本标记，因此：</font>```js``````text/jsx```

 <code><script type="text/jsx"></script></code> 

<font _mstmutation="1" _msthash="292682" _msttexthash="116002471">现在，让我们来了解一下我们的React代码！</font>

 <code>class HelloWorld extends React.Component {
  render() {
    // Tells React what HTML code to render
    return <h1>Hello World</h1>
  }
}

// Tells React to attach the HelloWorld component to the 'root' HTML div
ReactDOM.render(<HelloWorld />, document.getElementById("root"))</code> 

发生的只是"你好世界"显示为页面上的H1！

让我们来了解一下这里发生了什么。

<font _mstmutation="1" _msthash="291174" _msttexthash="335974665">首先，我们使用从类继承的 ES6 类。这是一个模式，我们将用于我们的大多数React组件。</font>```React.Component```

<font _mstmutation="1" _msthash="291473" _msttexthash="1177798895">接下来，我们类中有一个方法，它是一种称为 的特殊方法。React 会寻找方法以决定在页面上呈现什么内容。这个名字有道理。无论从该方法返回什么，都将由该组件呈现。</font>```render``````render``````render```

在这种情况下，我们将返回一个包含"Hello World"文本的 H1 ，这正是 HTML 文件中通常的内容。

<font _mstmutation="1" _msthash="292071" _msttexthash="33580872">最后，我们有：</font>

 <code>ReactDOM.render(<HelloWorld />, document.getElementById("root"))</code> 

我们使用 ReactDOM 功能将React组件附加到 DOM。

> <font _mstmutation="1" _msthash="760526" _msttexthash="2550696863">React 利用一种叫做虚拟 DOM 的东西，它是 DOM 的虚拟表示形式，您通常会在 Vanilla JavaScript 或 JQuery 中与之交互。这会将这个虚拟 DOM 呈现到实际的 DOM 中。 在场景后面， React 在界面上需要更改内容时， 会执行大量的工作来有效地编辑和重新呈现 DOM。</font>```reactDOM.render```

<font _mstmutation="1" _msthash="293267" _msttexthash="2231328593">我们的组件，看起来像一个HTML标签！此语法是_JSX 的一部分_，JSX 是 JavaScript 的扩展。您不能本机在浏览器中使用它。还记得我们如何使用巴别作为 JavaScript 吗？Babel 将转换（或转换）我们的JSX到常规JavaScript，以便浏览器能够理解它。</font>```<HelloWorld />```

> JSX 实际上是 React 中的可选选择，但在大多数情况下，您会看到它使用。

<font _mstmutation="1" _msthash="291161" _msttexthash="238278040">然后，我们使用 JavaScript 的内置功能来获取我们在 HTML 中创建的根元素。</font>```document.getElementById```

<font _mstmutation="1" _msthash="291460" _msttexthash="247257673">总之，在此语句中，我们将我们的组件附加到我们在 HTML 文件中创建的组件。</font>```ReactDOM.render``````HelloWorld``````div```

## [](#starter-code)<font _mstmutation="1" _msthash="305253" _msttexthash="15199197">初学者代码</font>

好了， 现在我们已经做了一个 "你好世界"， 我们可以开始我们的 Facebook 组件。

首先，我想让你玩这个演示。我们将在本教程的其余部分中对此进行处理。也请随意查看代码，但不要担心不理解它。这就是本教程的其余部分！

<font _mstmutation="1" _msthash="292955" _msttexthash="91846222">让我们从小部件的 HTML"硬编码"开始：</font>

 <code><div class="content">
  <div class="col-6 offset-3">
    <div class="card">
      <div class="card-block">
        <div class="row">
          <div class="col-2">
            <img src="https://zen-of-programming.com/react-intro/selfiesquare.jpg" class="profile-pic">
          </div>
          <div class="col-10 profile-row">
            <div class="row">
              <a href="#">The Zen of Programming</a>
            </div>
            <div class="row">
              <small class="post-time">10 mins</small>
            </div>
          </div>
        </div>
        <p>Hello World!</p>
        <div>
          <span class="fa-stack fa-sm">
            <i class="fa fa-circle fa-stack-2x blue-icon"></i>
            <i class="fa fa-thumbs-up fa-stack-1x fa-inverse"></i>
          </span>
        </div>
        <div>
          <hr class="remove-margin">
          <div>
            <button type="button" class="btn no-outline btn-secondary">
              <i class="fa fa-thumbs-o-up fa-4 align-middle" aria-hidden="true"></i>
              &nbsp;
              <span class="align-middle">Like</span>
            </button>
          </div>
        </div>
      </div>
      <div class="card-footer text-muted">
        <textarea class="form-control" placeholder="Write a comment..."></textarea>
        <small>120 Remaining</small>
      </div>
    </div>
  </div>
</div></code> 

对于一些添加的 CSS，如下所示：

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--hhLom4VO--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/7qps44tlmjx09di9u7l7.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--hhLom4VO--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/7qps44tlmjx09di9u7l7.png)

[下面是一个包含完整入门代码的 Codepen。](https://zshipu.com/t?url=https://codepen.io/aspittel/pen/KxzGdx)

<font _mstmutation="1" _msthash="291746" _msttexthash="1633763677">为了本教程，我们将创建四个组件：一个组件将成为父组件，一个包含喜欢逻辑的组件，以及包含用于键入注释的逻辑的组件。当您切换"喜欢"按钮时，组件还将有一个子级，该子项将显示或隐藏。</font>```Status``````Like``````Comment``````Like``````LikeIcon```

## [](#component-architecture)<font _mstmutation="1" _msthash="305552" _msttexthash="11606738">组件架构</font>

让我们继续将我们编写的 HTML 代码划分到这些组件中。

<font _mstmutation="1" _msthash="292643" _msttexthash="210032953">我们将从组件的外壳开始，我们将呈现它，以确保它的工作！</font>

 <code>class Status extends React.Component {
  render() {
    return (
      <div className="col-6 offset-3">
        <div className="card">
          <div className="card-block">
            <div className="row">
              <div className="col-10 profile-row">
                <div className="row">
                  <a href="#">The Zen of Programming</a>
                </div>
                <div class="row">
                  <small className="post-time">10 mins</small>
                </div>
              </div>
            </div>
          </div>
          <p>Hello world!</p>
          <div className="card-footer text-muted" />
        </div>
      </div>
    )
  }
}

ReactDOM.render(<Status />, document.getElementById("root"))</code> 

> 关于上述一个有趣的注意，是我们必须将"类"属性更改为"类名"。类在 JavaScript 中已经意味着一些东西 — — 它用于 es6 类！某些属性在 JSX 中的命名方式与在 HTML 中命名的方式不同。

<font _mstmutation="1" _msthash="293540" _msttexthash="316424446">我们还可以删除 HTML 的内容，只留下一个带 ID 根的元素 —— 父级"内容"div 只是为了样式化。</font>

 <code><body>
  <div class="content">
    <div id="root"></div>
  </div>
</body></code> 

下面是"状态"组件中的 HTML。请注意，一些原始 HTML 尚未存在 - 它将进入我们的子组件。

<font _mstmutation="1" _msthash="291733" _msttexthash="125465249">让我们创建第二个组件，然后将它包括在组件中。</font>```Status```

 <code>class Comment extends React.Component {
  render() {
    return (
      <div>
        <textarea className="form-control" placeholder="Write a comment..." />
        <small>140 Remaining</small>
      </div>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="292331" _msttexthash="1797093064">以下是我们评论的组件。它只是有我们的输入， 和文本与多少字符， 我们剩余。请注意，两者都包装在 中 ，这是因为 React 要求我们将组件的所有内容包装在一个 HTML 标记中 -- 如果我们没有父级，我们将返回 一个和标记。</font>```textarea``````div``````div``````textarea``````small```

<font _mstmutation="1" _msthash="292630" _msttexthash="830469341">因此，现在我们需要将这个组件包含在我们的组件中，因为它将是我们的子组件。我们可以使用我们用来呈现状态组件的相同 JSX 语法来做到这一点。</font>```Status```

 <code>class Status extends React.Component {
  render() {
    return (
      <div className="col-6 offset-3">
        <div className="card">
          <div className="card-block">
            <div className="row">
              <div className="col-10 profile-row">
                <div className="row">
                  <a href="#">The Zen of Programming</a>
                </div>
                <div className="row">
                  <small className="post-time">10 mins</small>
                </div>
              </div>
            </div>
          </div>
          <div className="card-footer text-muted">
+           <Comment />
          </div>
        </div>
      </div>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="293228" _msttexthash="102360245">好了， 现在我们只需要做同样的喜欢！</font>

 <code>class LikeIcon extends React.Component {
  render() {
    return (
      <div>
        <span className="fa-stack fa-sm">
          <i className="fa fa-circle fa-stack-2x blue-icon" />
          <i className="fa fa-thumbs-up fa-stack-1x fa-inverse" />
        </span>
      </div>
    )
  }
}

class Like extends React.Component {
  render() {
    return (
      <div>
        {/* Include the LikeIcon subcomponent within the Like component*/}
        <LikeIcon />
        <hr />
        <div>
          <button type="button">
            <i
              className="fa fa-thumbs-o-up fa-4 align-middle"
              aria-hidden="true"
            />
            &nbsp;
            <span className="align-middle">Like</span>
          </button>
        </div>
      </div>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="293826" _msttexthash="109397769">然后，我们需要包括在我们的原始组件！</font>```Status```

 <code>class Status extends React.Component {
  render() {
    return (
      <div className="col-6 offset-3">
        <div className="card">
          <div className="card-block">
            <div className="row">
              <div className="col-10 profile-row">
                <div className="row">
                  <a href="#">The Zen of Programming</a>
                </div>
                <div className="row">
                  <small className="post-time">10 mins</small>
                </div>
              </div>
            </div>
+           <Like />
          </div>
          <div className="card-footer text-muted">
            <Comment />
          </div>
        </div>
      </div>
    )
  }
}</code> 

酷， 现在我们已经React化了我们原来的 Html， 但它仍然什么都不做！我们开始修复它吧！

总之，本节中的代码将看起来像此[CodePen！](https://zshipu.com/t?url=https://codepen.io/aspittel/pen/yxOQMe?editors=0010)

## [](#state-and-props)<font _mstmutation="1" _msthash="305838" _msttexthash="11471655">州和道具</font>

我们有两个不同的用户交互，我们要实现：

*   我们希望只有在按下"喜欢"按钮时才显示"喜欢"图标
*   我们希望剩余字符数作为人减少

让我们开始研究这些吧！

### [](#props)<font _mstmutation="1" _msthash="307359" _msttexthash="5531097">道具</font>

假设我们希望我们的注释框允许不同位置的字母数量不同。例如，在状态上，我们希望允许用户编写 200 个字母长的响应。但是，在图片上，我们只希望他们能够编写 100 个字符的响应。

<font _mstmutation="1" _msthash="294112" _msttexthash="753103598">React 允许我们从组件和组件传递道具（属性的短），以指定我们想要在响应中允许的字母数，而不是具有两个不同的注释组件。</font>```PictureStatus``````Status```

<font _mstmutation="1" _msthash="294411" _msttexthash="48885707">道具的语法如下所示：</font>

 <code><Comment maxLetters={20} />
<Comment text='hello world' />
<Comment show={false} />

var test = 'hello world'
<Comment text={test} /></code> 

道具看起来像 HTML 属性！如果通过道具传递字符串，则不需要括号，但任何其他数据类型或变量都需要在括号内。

<font _mstmutation="1" _msthash="292604" _msttexthash="162311799">然后，在我们的组件中，我们可以使用我们的道具：</font>

 <code>console.log(this.props.maxLetters)</code> 

<font _mstmutation="1" _msthash="293202" _msttexthash="138863478">它们捆绑在实例的属性中，以便可以使用 访问它们。</font>```props``````this.props.myPropName```

因此，让我们更改硬编码的 140 个字符，以便于在组件外部更改。

<font _mstmutation="1" _msthash="293800" _msttexthash="324076948">首先，我们将更改状态组件中实例化注释组件的地点（请注意省略了一些代码！</font>

 <code>class Status extends React.Component {
        ...
          <div className="card-footer text-muted">
+            <Comment maxLetters={280} />
          </div>
        </div>
      </div>
    )
  }
}</code> 

<font _mstmutation="1" _msthash="294398" _msttexthash="165188322">然后，我们将更改注释组件中的硬编码 140 个字符的限制。</font>

 <code>class Comment extends React.Component {
  ...
        <div>
        <textarea className="form-control" placeholder="Write a comment..." />
+       <small>{this.props.maxLetters} Remaining</small>
      </div>
  ...
}</code> 

### [](#state)<font _mstmutation="1" _msthash="308906" _msttexthash="5228314">状态</font>

我们从组件传递到组件的道具永远不会_在子_组件内更改 —— 它们可以在父组件内更改，但在子组件内可以更改。但是 --很多时候，我们将具有在组件生命周期内想要更改的属性。例如，我们希望记录用户在文本区域中键入的字符数，并且我们希望跟踪状态是否"喜欢"。我们将存储那些要在其状态的组件中更改_的属性_。

> 你会注意到 React 中的很多不变性 —— 它受到功能范式的影响很大，因此也不鼓励副作用。

我们希望每当我们创建组件的新实例时都会创建此状态，因此我们将使用 ES6 类构造函数来创建它。如果你想快速刷新ES6类[MDN是](https://zshipu.com/t?url=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)一个伟大的资源。

<font _mstmutation="1" _msthash="305929" _msttexthash="798243420">State 将是具有我们想要包含的任何键值对的对象。在这种情况下，我们需要一个字符计数的用户键入的字符数。我们现在将设置为零。</font>

 <code>class Comment extends React.Component {
  constructor () {
    super()
    this.state = {
      characterCount: 0
    }
  }
  ...</code> 

<font _mstmutation="1" _msthash="306553" _msttexthash="270961288">现在，让我们从道具中减去它，所以我们总是知道我们还剩多少个字符！</font>```maxLetters```

 <code><small>{this.props.maxLetters - this.state.characterCount} Remaining</small></code> 

<font _mstmutation="1" _msthash="307177" _msttexthash="83860972">如果增加 ，则剩余的显示字符将减少。</font>```characterCount```

<font _mstmutation="1" _msthash="307489" _msttexthash="551751395">但是 - 键入时没有任何React。我们永远不会改变 的值。我们需要向 添加一个事件处理程序，以便我们更改用户类型时。</font>```characterCount``````textarea``````characterCount```

### [](#event-handlers)<font _mstmutation="1" _msthash="322231" _msttexthash="18703490">事件处理程序</font>

过去编写 JavaScript 时，您可能已编写事件处理程序以与用户输入进行交互。我们将在 React 中做同样的事情，语法只是会有点不同。

<font _mstmutation="1" _msthash="305604" _msttexthash="563139798">我们将向 中添加一个处理程序。在其中，我们将对事件处理方法进行引用，该方法将在 每次用户在 中输入时运行。</font>```onChange``````textarea``````textarea```

  <code><textarea className="form-control" placeholder="Write a comment..." onChange={this.handleChange}/></code> 

<font _mstmutation="1" _msthash="306228" _msttexthash="66036789">现在我们需要创建一个方法：</font>```handleChange```

 <code>class Comment extends React.Component {
  constructor () {
    super()
    this.state = {
      characterCount: 0
    }
  }

  handleChange (event) {
    console.log(event.target.value)
  }
...</code> 

<font _mstmutation="1" _msthash="306852" _msttexthash="1816697857">现在，我们只是-ing - 这将工作的方式与它在无ReactJavaScript中的工作方式相同（不过，如果你深入一点，事件对象就有点不同了）。如果你看看那个控制台， 我们正在打印出我们在文本框中键入的内容！</font>```console.log``````event.target.value```

<font _mstmutation="1" _msthash="307164" _msttexthash="810537650">现在我们需要更新处于状态的属性。在 React 中_，我们从不直接_修改状态 ，因此我们不能做类似的事情： 。相反，我们需要使用该方法。</font>```characterCount``````this.state.characterCount = event.target.value.length``````this.setState```

  <code>handleChange (event) {
    this.setState({
      characterCount: event.target.value.length
    })
  }</code> 

<font _mstmutation="1" _msthash="307788" _msttexthash="2453919117">但！您会收到一个错误 -- "未捕获的 TypeRror： this.setState 不是函数"。此错误告诉我们，需要在事件处理程序中保留 es6 类的上下文。我们可以通过绑定到构造函数中的方法来做到这一点。如果你想阅读更多关于这个，[这里有一篇好文章](https://zshipu.com/t?url=https://medium.freecodecamp.org/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb)。</font>```this```

 <code>class Comment extends React.Component {
  constructor () {
    super()    
    this.handleChange = this.handleChange.bind(this)
...</code> 

<font _mstmutation="1" _msthash="305591" _msttexthash="147231448">好！我们快到了！我们只需要添加切换显示的能力。</font>```like```

<font _mstmutation="1" _msthash="305903" _msttexthash="707616884">我们需要向组件添加一个构造函数。在该构造函数中，我们需要实例化组件的状态。组件生命周期内将发生的变化是状态是否被喜欢。</font>```Like```

 <code>class Like extends React.Component {
  constructor() {
    super()

    this.state = {
      liked: false
    }
  }
  ...</code> 

<font _mstmutation="1" _msthash="306527" _msttexthash="176152769">现在我们需要添加一个事件处理程序来更改状态是否被喜欢。</font>

 <code>class Like extends React.Component {
  constructor() {
    super()

    this.state = {
      liked: false
    }

    this.toggleLike = this.toggleLike.bind(this)
  }

  toggleLike () {
    this.setState(previousState => ({
      liked: !previousState.liked
    }))
  }
...</code> 

<font _mstmutation="1" _msthash="307151" _msttexthash="952978299">这里的区别在于，接收参数的回调函数-- .正如您可能从参数的名称中猜到的，这是调用之前的状态值。 是异步的，所以我们不能依赖于在它里面使用。</font>```this.setState``````previousState``````this.setState``````setState``````this.state.liked```

现在，我们需要：

<font _mstmutation="1" _msthash="307775" _msttexthash="258916450">a） 每当用户单击"喜欢"按钮时调用事件处理程序：
b） 仅在为 true 时显示 Likeicon</font>```liked```

  <code>render() {
    return (
      <div>
        {/* Use boolean logic to only render the LikeIcon if liked is true */}
+       {this.state.liked && <LikeIcon />}
        <hr />
        <div>
+          <button type="button" className="btn no-outline btn-secondary" onClick={this.toggleLike}>
            <i
              className="fa fa-thumbs-o-up fa-4 align-middle"
              aria-hidden="true"
            />
            &nbsp;
            <span className="align-middle">Like</span>
          </button>
        </div>
      </div>
    )
  }</code> 

棒！现在，我们所有的功能都到位了。

## [](#bonus-functional-components)<font _mstmutation="1" _msthash="319969" _msttexthash="27873859">奖励：功能组件</font>

如果你觉得你已经在你的头上，请随时跳过这部分，但我想使一个快速重构这个项目。如果我们创建没有与其关联的状态的组件（我们称之为无状态组件），我们可以将组件转换为函数而不是 ES6 类。

<font _mstmutation="1" _msthash="306514" _msttexthash="114802974">在这种情况下，我们可以看起来像这样：</font>```LikeIcon```

 <code>const LikeIcon = () => {
  return (
    <div>
      <span className="fa-stack fa-sm">
        <i className="fa fa-circle fa-stack-2x blue-icon" />
        <i className="fa fa-thumbs-up fa-stack-1x fa-inverse" />
      </span>
    </div>
  )
}</code> 

<font _mstmutation="1" _msthash="307138" _msttexthash="105980758">我们只是返回组件的 UI，而不是使用 方法。</font>```render```

[下面是](https://zshipu.com/t?url=https://codepen.io/aspittel/pen/NLrPWN)实现此重构的 CodePen。

## [](#cheat-sheet)<font _mstmutation="1" _msthash="321919" _msttexthash="7121686">备忘单</font>

我喜欢备忘单， 所以我做了一个从这篇文章的内容！

[![React cheat sheet with state and props, event handlers, and components](https://res.cloudinary.com/practicaldev/image/fetch/s--PDiR6TPA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/t1321qej0f0gsz1u5bok.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--PDiR6TPA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/t1321qej0f0gsz1u5bok.png)

您也可以在这里下载它作为[PDF！](https://zshipu.com/t?url=https://zen-of-programming.com/react-intro/cheatsheet.pdf)

## [](#next-steps)<font _mstmutation="1" _msthash="320281" _msttexthash="6619015">步骤</font>

回顾一下，我们讨论了组件体系结构、基本 React 语法和 JSX、状态和道具、事件处理程序和功能组件。

如果您想查看本教程中的所有 CodePens，下面是[一](https://zshipu.com/t?url=https://codepen.io/collection/XpPbVv/)个集合！

如果您想尝试从本教程中扩展代码，我建议将赞更改为React或创建一个照片组件，以重用我们制作的某些组件！

