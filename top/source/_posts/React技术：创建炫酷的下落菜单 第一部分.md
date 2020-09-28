
title: React技术：创建炫酷的下落菜单 第一部分
author: 知识铺
date: 2020-09-28 22:17:20
tags: 
---
 一个小下拉菜单扔在你网站的一个紧张的区域怎么样？或者使用它作为一个简单的导航工具与你的简约布局？当屏幕缩小到更小时，可能会使用此较小的菜单。

[![dropdown demo](https://res.cloudinary.com/practicaldev/image/fetch/s--9m0XgPab--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/nglfi1orf9r3dc2q7vlc.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--9m0XgPab--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/nglfi1orf9r3dc2q7vlc.gif)

> [Github 上的代码](https://zshipu.com/t?url=https://github.com/cooljasonmelton/dropdown)

### [](#tutorial)<font _mstmutation="1" _msthash="289926" _msttexthash="5610267">教程</font>

##### [](#table-of-contents)<font _mstmutation="1" _msthash="290771" _msttexthash="5308706">目录</font>

*初步垃
圾 *
菜单组件 *
菜单CSS
*React路由器*结论

##### [](#preliminary-junk)<font _mstmutation="1" _msthash="291369" _msttexthash="10296754">初步垃圾</font>

<font _mstmutation="1" _msthash="277953" _msttexthash="678840955">为了得到它去，我做了一个，安装了[React](https://zshipu.com/t?url=https://reactrouter.com/web/guides/quick-start)路由器，删除了任何不必要的默认代码，并设置了一个文件结构，如下所示：</font>```create-react-app```

[![file structure](https://res.cloudinary.com/practicaldev/image/fetch/s--4EKMpKTf--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/yvzl49av9qe3te5otbqa.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--4EKMpKTf--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/yvzl49av9qe3te5otbqa.png)

##### [](#menu-component)<font _mstmutation="1" _msthash="304564" _msttexthash="11715132">菜单组件</font>

```Menu.js```<font _mstmutation="1" _msthash="290615" _msttexthash="45573112">包含下拉列表的所有 JavaScript 和 JSX。</font>

基本上有四个部分：

1.  <font _mstmutation="1" _msthash="582920" _msttexthash="205941216">一个挂钩，它拿着一个布尔，指示菜单是否应该打开。我称之为 。</font>```useState``````openMenu```

2.  <font _mstmutation="1" _msthash="583297" _msttexthash="271825060">称为该函数，该函数有条件地将类添加到菜单项。类的 CSS 将为菜单设置动画。</font>```setClassNames()```

3.  <font _mstmutation="1" _msthash="583674" _msttexthash="204478417">称为函数，它使用 React 路由器将相关组件呈现到单击的菜单项。</font>```pushToRoute()```

4.  <font _mstmutation="1" _msthash="584051" _msttexthash="126517963">组件返回 JSX，用于呈现结构并汇集所有功能。</font>```Menu```

 <code>import React, {useState} from 'react';

// router
import { withRouter } from 'react-router-dom';

// styling
import './Menu.css';

const Menu = props => {
    // conditionally render dropdown affect based on this boolean
    const [openMenu, setOpenMenu] = useState(false)

    // parameter num corresponds to .open-# classes
    // is assigned when Menu clicked triggering animated dropdown
    const setClassNames = num => {
        const classArr = ["m-item"];
        if (openMenu) classArr.push(`open-${num}`)
        return classArr.join('  ')
    }

    // takes route string as parameter
    const pushToRoute = route => {
        props.history.push(route)
        setOpenMenu(false)
    }

    return (
        <div className="Menu">
            <div className={"m-item m-logo"}
                onClick={() => setOpenMenu(!openMenu)}>
                Menu
            </div>
            <div className={setClassNames(1)}
                onClick={() => pushToRoute("/dashboard")}>
                Dashboard
            </div>
            <div className={setClassNames(2)}
                onClick={() => pushToRoute("/settings")}>
                Settings
            </div>
            <div className={setClassNames(3)}
                onClick={() => pushToRoute("/")}>
                Sign out
            </div>
        </div>
  );
}

export default withRouter(Menu);</code> 

##### [](#menu-css)<font _mstmutation="1" _msthash="306124" _msttexthash="5320926">菜单 CSS</font>

[![dropdown menu](https://res.cloudinary.com/practicaldev/image/fetch/s--QBGaLF0f--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/h6nwgyc1jise7pihzk5t.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--QBGaLF0f--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/h6nwgyc1jise7pihzk5t.png)

CSS 完成打开菜单的所有工作。有五个重要部分。

<font _mstmutation="1" _msthash="292708" _msttexthash="68783832">1 类是最外部的容器。此层需要 。</font>```.Menu``````position: relative;```

<font _mstmutation="1" _msthash="290303" _msttexthash="384973849">各个菜单项将具有 ，因此它们将基于具有 的最近组件进行渲染。位置的基础将是组件的外部 div。</font>```position: absolute;``````position``````Menu```

<font _mstmutation="1" _msthash="290602" _msttexthash="422344260">2 类应用于每个单独的菜单项。他们绝对定位与初始。这将在 div 的顶部呈现彼此顶部的所有项目。</font>```.m-item``````top: 0;``````.Menu```

<font _mstmutation="1" _msthash="290901" _msttexthash="651361438">我使用单位和所有其他属性，因此我可以确保项目将完全适合彼此的顶部，仍然响应（单位是相对于元素的字体大小）。</font>```em``````width``````em```

<font _mstmutation="1" _msthash="291200" _msttexthash="103830948">对于美学，我给他们一个，，，和 。</font>```background-color``````box-shadow``````padding``````border-radius``````font-size``````color```

<font _mstmutation="1" _msthash="291499" _msttexthash="371478640">属性将文本垂直和水平居中。 更改屏幕上鼠标指针的样式，以显示用户菜单项是可单击的。</font>```flexbox``````cursor```

<font _mstmutation="1" _msthash="291798" _msttexthash="84774352">最后，将动画更改属性应用的函数和CSS 。</font>```transition``````setClassNames()``````:hover```

 <code>.Menu{
    position: relative;
    margin: 2em 3em;
}

.m-item{
    position: absolute;
    top: 0;

    width: 5.5em;
    background-color: #301A4B;
    box-shadow: 1px 2px 2px #301A4B;

    padding: 0.2em;

    border-radius: 1em;

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 1.5em;
    color: #EDFFEC;
    cursor: pointer;

    transition: 1s;
}</code> 

<font _mstmutation="1" _msthash="292396" _msttexthash="375426922">3 在悬停时向菜单项添加一个小边框。添加的 1 px 边框使项目稍微动画，给他们一点点生命。</font>```.m-item:hover```

 <code>.m-item:hover{
    border: 1px solid black;
}</code> 

<font _mstmutation="1" _msthash="292994" _msttexthash="322251709">4 是第一个菜单项的特殊类。将此 div 带到顶部，以便所有其他 div 可以隐藏在它下面。</font>```.m-logo``````z-index: 1;```

```z-index```<font _mstmutation="1" _msthash="290589" _msttexthash="335601266">默认值为 0，因此如果只有一个项目声明它，则 1 将足以将它带到所有其他项的顶部。</font>

 <code>.m-logo{
    z-index: 1;
}</code> 

<font _mstmutation="1" _msthash="291187" _msttexthash="276175549">5 一系列类称为 ，并导致下拉的动画。这些类通过单击顶部菜单项时应用。</font>```.open-1``````.open-2``````.open-3``````setClassNames()```

<font _mstmutation="1" _msthash="291486" _msttexthash="330383950">单击时，每个项将转换到其类中的新属性。也就是说，它们将移动到新指定的 和新的 。</font>```open-#``````top``````background-color```

 <code>.open-1{
    top: 1.8em;
    background-color: #9b5de5;
}
.open-2{
    top: 3.6em;
    background-color: #f15bb5;
}
.open-3{
    top: 5.4em;
    background-color: #00BBF9;
}</code> 

##### [](#react-router)<font _mstmutation="1" _msthash="306410" _msttexthash="15784756">React路由器</font>

此时设置了菜单组件的所有美学方面。剩下的是设置React路由器，以便单击项目将导航到正确的组件。

我分三步连线：

<font _mstmutation="1" _msthash="292981" _msttexthash="264651478">1 该文件是整个项目的主运行文件，所以这是我设置基本路由器的东西。</font>```App.js```

<font _mstmutation="1" _msthash="293280" _msttexthash="241158827">我包装应用程序的回报，以便即将推出的路由将可用于包含的所有组件。</font>```BrowserRouter```

<font _mstmutation="1" _msthash="290875" _msttexthash="897027599">我设置了 一个，以便当呈现一个路由时，其他路由将被禁用。在 内部，我定义项目所需的每个特定路由（为了演示，这些路由设置为）。</font>```Switch``````null```

<font _mstmutation="1" _msthash="291174" _msttexthash="550800640">组件放置在 外部，以便每当呈现时都会呈现。这使得它成为一个高效的导航工具，可在应用程序的任何屏幕上使用。</font>```Menu``````Switch``````App```

 <code>import React from 'react';

// router
import { BrowserRouter, Route, Switch } from 'react-router-dom';

// styling
import './App.css';

// components
import Menu from './Menu/Menu';

const App = () => {
  return (
    <BrowserRouter>
      <div className="App">
        {/* dropdown menu */}
        <Menu/>
        {/* routes */}
        <Switch>
          <Route exact path="/settings" component={null} />
          <Route exact path="/dashboard" component={null} />
          <Route exact path="/" component={null} />
        </Switch>
      </div>
    </BrowserRouter>
  );
}

export default App;</code> 

<font _mstmutation="1" _msthash="291772" _msttexthash="166681203">2 在我们的菜单组件中，我在导出语句中导入并包装菜单。</font>```withRouter```

 <code>// router
import { withRouter } from 'react-router-dom';</code> 

 <code>export default withRouter(Menu);</code> 

```withRouter```<font _mstmutation="1" _msthash="292669" _msttexthash="239015920">给道具，将使我们能够操纵。为了访问这些 参数，我们给出 的参数为 。</font>```Menu``````react-router-dom``````Menu``````props```

 <code>const Menu = props => {</code> 

<font _mstmutation="1" _msthash="293267" _msttexthash="649992096">3 最后，我写了一个函数，它采用路由的参数字符串，并推送我们的应用程序到该路由。然后，它通过调用 关闭菜单。</font>```pushToRoute()``````setOpenMen(false)```

  <code>// takes route string as parameter
    const pushToRoute = route => {
        props.history.push(route)
        setOpenMenu(false)
    }</code> 

<font _mstmutation="1" _msthash="291161" _msttexthash="64414545">菜单项在单击时调用。
例如：</font>```pushToRoute()```

  <code><div className={setClassNames(1)}
        onClick={() => pushToRoute("/dashboard")}>
        Dashboard
   </div></code> 

##### [](#conclusion)<font _mstmutation="1" _msthash="306072" _msttexthash="6674577">结论</font>

我喜欢创建这个菜单。它是一种高效且易于编写代码的工具，可以在许多方案中提供帮助。我希望你发现这些概念很有用。



