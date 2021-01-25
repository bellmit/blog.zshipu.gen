
---
title: React设计模式（第 1 部分）
author: 知识铺
date: 2021-01-25 22:00:25+08:00
tags: []
---

<font _mstmutation="1" _msthash="276523" _msttexthash="522377011">**注：**有些模式侧重于状态管理概念，但我们可以避免和其他第三方状态管理工具，因为它们与本文的主题无关。</font>```Redux,``````Mobx```

## [](#render-props)<font _mstmutation="1" _msthash="289653" _msttexthash="12365275">渲染道具</font>

响应文档[比比皆是](https://zshipu.com/t?url=https://reactjs.org/docs/render-props.html)：

> 术语"呈现道具"是指使用其值为函数的 prop 在 React 组件之间共享代码的技术。

<font _mstmutation="1" _msthash="277667" _msttexthash="333457280">简单地说，**它只是一个函数值的道具。函数是需要呈现的组件**。也许你已经看到了：</font>```React Router```

 <code><Route
  path='/about'
  render={(props) => (
    <About {...props} isLoad={true} />
  )}
/></code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1007968" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1008514" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

此模式的主要目的是**更新同级组件的道具**。它使组件更可重用，并帮助我们更容易[实现"关注点](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/Separation_of_concerns)分离"。

让我们以以下方案为例：

*   <font _mstmutation="1" _msthash="462358" _msttexthash="40574859">我们需要开发一个组件。</font>```Form```
*   <font _mstmutation="1" _msthash="462735" _msttexthash="22216090">里面我们有 和 。</font>```From``````p``````input```
*   <font _mstmutation="1" _msthash="463112" _msttexthash="22969115">是用户的输入。</font>```input```
*   <font _mstmutation="1" _msthash="463489" _msttexthash="30154280">显示了用户写入的。</font>```p```

<font _mstmutation="1" _msthash="290914" _msttexthash="79843114">我们可以简单地创建类似的东西：</font>

 <code>import React, { useState } from "react";
export default function Input(props) {
  return (
    <>
      <input
        type="text"
        value={props.value}
        onChange={props.onChange}
      />
    </>
  );
}

export default function Form() {
  const [value, setValue] = useState("");
  return (
    <form>
      <Input onChange={e => setValue(e.target.value)}/>
      <p>{value}</p>
    </form>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042522" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043081" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

此方法存在两个问题：

<font _mstmutation="1" _msthash="291811" _msttexthash="225741620">1\. 在这种情况下，我们不使用"关注点"概念，因为 应控制 和 而不是 。</font>```Input``````Value``````Form```

2\. 我们的组件不太可重复使用和灵活。

<font _mstmutation="1" _msthash="292409" _msttexthash="139135958">我们可以重构代码并使用**渲染道具**，像这样：</font>

 <code>import React, { useState } from "react";

function Input(props) {
  const [value, setValue] = useState("");
  return (
    <>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      {props.render && props.render(value)}
    </>
  );
}

export default function Form() {
  return (
    <form>
      <Input render={(value) => <p>{value}</p>} />
    </form>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044147" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044706" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="290303" _msttexthash="317176496">这样，组件控制值，并且它更可重用（相同的功能可以使用不同的元素实现）。</font>```Input```

## [](#hoc-higherorder-components)<font _mstmutation="1" _msthash="304044" _msttexthash="20859137">HOC - 高阶组件</font>

```Higher-Order Components```<font _mstmutation="1" _msthash="290901" _msttexthash="571596636">基本上是一个函数，该函数接收组件作为参数，并返回具有特定业务逻辑的新组件。你可能在 "Redux" 中看到了这一点：</font>

 <code>export default connect(mapStateToProps , mapDispatchToProps)(From);</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042509" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043068" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291499" _msttexthash="423008430">使用 ，您可以编写单独的功能到应用的公域（全局）功能，并在项目中的衍射组件上重用它。</font>```Higher-Order Components```

让我们采取另一个场景：

*   <font _mstmutation="1" _msthash="463905" _msttexthash="40580943">我们需要开发两个组件。</font>```menu```
*   <font _mstmutation="1" _msthash="464282" _msttexthash="148502874">在第一个组件中，我们有一个需要阻止菜单单击事件。</font>```button```
*   <font _mstmutation="1" _msthash="464659" _msttexthash="149221345">第二个组件也是 ，但这次我们需要_处理菜单_单击事件。</font>```button```

问题是我们需要两**种菜单-一种是具有停止```传播能力的菜单，```另一种是没有停止的菜单。**

<font _mstmutation="1" _msthash="292695" _msttexthash="40585792">我们可以这样使用：</font>```Higher-Order Components```

 <code>import React from "react";
import "./style.css";

function stopPropagation(WrappedComponent) {
  return function(){
    const handleClick = event => {
      event.stopPropagation();
      WrappedComponent.handleClick()
    };
     return <WrappedComponent onClick={handleClick} />;
  }
}

function Button(props){
  const handleClick = () => console.log("button clicked!");
  Button.handleClick = handleClick; 
  return <button onClick={props.onClick || handleClick}>Click Me</button>;
}

function Menu(props) {
  const openMenu = () => console.log("menu opened!");
  return (
    <div onClick={openMenu} className="menu">
      <h1>Menu</h1>
      {props.children}
    </div>
  );
}

export default function App() {
  const ButtonPropagation = stopPropagation(Button);
  return (
    <div>
      <Menu>
        <ButtonPropagation />
      </Menu>
      <Menu>
        <Button />
      </Menu>
    </div>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044459" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045018" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

[链接到演示](https://zshipu.com/t?url=https://stackblitz.com/edit/react-hfen5s?file=src/App.js)

让我们分析一下此代码：

*   <font _mstmutation="1" _msthash="462956" _msttexthash="44302752">组件读取我们提到的两个。</font>```App``````Menus```
*   <font _mstmutation="1" _msthash="463333" _msttexthash="82537481">组件读取标题和子（本例中为 ）。</font>```Menu``````Button```
*   ```Button```<font _mstmutation="1" _msthash="463710" _msttexthash="351432133">具有具有单击事件的按钮元素。 * 我们需要使用导出此函数（在类组件中，您可以使用 。</font>```**handleClick``````Button.handleClick= handleClick``````static```
*   <font _mstmutation="1" _msthash="464087" _msttexthash="582222927">**```止损推进```是高阶组件**。它接收一个组件（在我们的情况下），并发送回具有新能力的组件（在我们的情况下）。</font>```Button``````stopPropagation```

<font _mstmutation="1" _msthash="291486" _msttexthash="819672204">这是使用 的简单示例。我们可以使用，不需要在不同的组件上再次重写。更重要的是，我们可以创建其他"按钮"HOC，如防止防御和队列点击。</font>```Higher-Order Components``````stopPropagation```

