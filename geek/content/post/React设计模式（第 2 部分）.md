
---
title: React设计模式（第 2 部分）
author: 知识铺
date: 2021-01-25 22:04:18+08:00
tags: []
---


<font _mstmutation="1" _msthash="276523" _msttexthash="93062034">这一次，我们将讨论模式、模式和模式。</font>```Context``````Presentational and Container Components``````Compound Components```

## [](#context)<font _mstmutation="1" _msthash="289653" _msttexthash="6936761">上下文</font>

根据React[文档](https://zshipu.com/t?url=https://reactjs.org/docs/context.html)：

> 上下文提供了一种通过组件树传递数据的方法，而无需在每个级别手动传递道具。

<font _mstmutation="1" _msthash="277667" _msttexthash="775808865">简单地说，如果您有一个需要通过多个组件级别的全局状态，可以使用 。例如：如果您有一个会影响所有组件的组件，将简化该过程。</font>```Context``````theme``````Context```

<font _mstmutation="1" _msthash="277953" _msttexthash="1558016486">**注意。**使用时有一个潜在的障碍需要牢记：它可以降低组件的可重用性。数据将在作用域中可用，因此不能在 外部使用它。我找到了一个很棒的[视频](https://zshipu.com/t?url=https://www.youtube.com/watch?v=3XaXKiXtNjw&ab_channel=ReactTraining)来解释这个问题， 并告诉你如何避免 "道具钻探" 。</font>```Context``````Context``````Provider``````Provider```

<font _mstmutation="1" _msthash="290017" _msttexthash="87350653">让我们看一个上下文在行动的示例：</font>

 <code>import React, { useContext, createContext } from "react";
import "./styles.css";
let data = {
  title: "Welcome"
};
const Context = createContext();

export default function App() {
  return (
    <Context.Provider value={data}>
      <div className="App">
        <Card />
      </div>
    </Context.Provider>
  );
}

const Card = () => {
  return (
    <div className="card">
      <CardItem />
    </div>
  );
};

const CardItem = () => {
  return (
    <div className="CardItem">
      <Title />
    </div>
  );
};

const Title = () => {
  const data = useContext(Context);
  return <h1>{data.title}</h1>;
};</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1041547" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1042106" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="290615" _msttexthash="867760777">正如我们在这个（基本）示例中看到的，我们有三个级别的组件，并且我们只使用最后一个级别的 。这样，我们不需要把道具传递给所有级别。</font>```data.title```

### [](#a-few-tips-on-context-syntax)<font _mstmutation="1" _msthash="304642" _msttexthash="50026977">有关上下文语法的一些提示</font>

使用上下文时，我总是应用此语法。然而，当我再次写的时候，我发现一些事情：

*   <font _mstmutation="1" _msthash="463294" _msttexthash="345545785">在"静态数据"（如示例）中，我们实际上不需要 。我们可以自己履行这一职能：</font>```Provider```

 <code>let data = {
  title: "Welcome"
};
const Context = createContext(data);

export default function App() {
  return (
    <div className="App">
      <Card />
    </div>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043172" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043731" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292110" _msttexthash="161175222">在比例的另一端，我们可以使用 而不是 ， 像这样：</font>```Customer``````useContext```

 <code>const Title = () => {
  return (<Context.Consumer>
            {(data) => <h1>{data.title}</h1>}
        </Context.Consumer>);
};</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043822" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044381" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

## [](#presentational-and-container-components)<font _mstmutation="1" _msthash="306241" _msttexthash="23041928">演示和容器组件</font>

<font _mstmutation="1" _msthash="290303" _msttexthash="508927692">这些组件（也称为 ）是最著名的React模式之一。React 文档中没有引用它们，但 Dan Abramov 的文章[提供了](https://zshipu.com/t?url=https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)出色的指南。</font>```Smart And Dumb Components```

<font _mstmutation="1" _msthash="290602" _msttexthash="133579784">简单地说，请参阅业务逻辑组件与 UI 视图的分离。</font>```Presentational And Container Components```

让我们看看另一个场景：

*   <font _mstmutation="1" _msthash="462969" _msttexthash="41332291">我们需要构建一个组件。</font>```Card```
*   <font _mstmutation="1" _msthash="463346" _msttexthash="91299247">在卡内，我们还有三个其他组件： 和 。</font>```Title``````Image``````Button```
*   单击后，该按钮将更改图片。

<font _mstmutation="1" _msthash="291499" _msttexthash="423489404">在开始处理组件之前，让我们创建两个文件夹："演示"和"容器"。现在，让我们构建三个组件：</font>```Presentational```

**标题.js ：**

 <code>import React from "react";
export default function Title(props) {
  const { children, ...attributes } = props;
  return <h1 {...attributes}>{children}</h1>;
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043484" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044043" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

**图片.js ：**

 <code>import React from "react";
export default function Image(props) {
  const { src, alt } = props || {};
  return <img src={src} alt={alt} />;
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044134" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044693" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

**按钮.js ：**

 <code>import React from "react";
export default function Button(props) {
  const { children, ...attributes } = props;
  return <button {...attributes}>{children}</button>;
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1041846" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1042405" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="290888" _msttexthash="134301583">最后，我们可以在容器文件夹组件中生成，称为 。</font>```Card```

**卡.js ：**

 <code>import React, { useEffect, useState } from "react";
import Title from "../Presentational/Title";
import Image from "../Presentational/Image";
import Button from "../Presentational/Button";

export default function Card() {
  const [card, setCard] = useState({});
  const [srcIndex, setSrcIndex] = useState(0);

  useEffect(() => {
    setCard({
      title: "Card Title",
      image: {
        imagesArray: [
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTh87QN4DkF7s92IFSfm7b7S4IR6kTdzIlhbw&usqp=CAU",
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRjFnHdaH1i1m_xOaJfXTyq4anRFwRyCg1p1Q&usqp=CAU"
        ],
        alt: "card image"
      }
    });
  }, []);
  const { image } = card;
  const changeImage = () =>
    setSrcIndex((index) =>
      index < image.imagesArray.length - 1 ? index + 1 : index - 1
    );
  return (
    <div className="card">
      <Title className="title-black">{card.title && card.title}</Title>
      <Image
        src={image && image.imagesArray[srcIndex]}
        alt={image && image.alt}
      />
      <Button onClick={changeImage}>Change Picture</Button>
    </div>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042821" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043380" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

如果您想查看完整的代码，请在此处[查看](https://zshipu.com/t?url=https://codesandbox.io/s/presentational-and-container-component-example-9df6h)。

<font _mstmutation="1" _msthash="292084" _msttexthash="394290689">**注意！**你们很多人可能想知道为什么需要分成不同的组件。你可以把它们写在里面，对吗？</font>```Card```

<font _mstmutation="1" _msthash="292383" _msttexthash="509711085">当我们分离组件时，我们可以在任何地方重用它们。但更重要的是，实现其他模式（如 或 ）要容易得多。</font>```HOC``````Render Props```

## [](#compound-components)<font _mstmutation="1" _msthash="306215" _msttexthash="9978683">复合成分</font>

在我看来，这是最复杂的模式之一，要理解，但我会尽量简单地解释它。

<font _mstmutation="1" _msthash="293280" _msttexthash="1060014696">当我们谈论 时，最简单的方法是思考和使用HTML。您可以将它们视为具有基本功能的一组组件。有些状态是全局（如在模式中）或从容器（如模式）管理的。</font>```Compound Components``````select``````option``````context``````presentational and container```

**```复合成分```**是这两者的混合体。这几乎就像他们每个人都有自己的状态， 他们从内部管理他们。

让我们看看下一个场景：

*   <font _mstmutation="1" _msthash="463255" _msttexthash="36371855">我们需要开发和组件。</font>```Select``````Option```
*   <font _mstmutation="1" _msthash="463632" _msttexthash="62883626">我们希望生动，不同的颜色。</font>```Option```
*   <font _mstmutation="1" _msthash="464009" _msttexthash="29653065">颜色会影响颜色。</font>```Option``````Select```

让我们看看示例：

**应用程序.js**

 <code>import React from "react";
import "./styles.css";
import Select from "./Select";
import Option from "./Option";

export default function App() {
  return (
    <div>
      <Select>
        <Option.Blue>option 1</Option.Blue>
        <Option.Red>option 2</Option.Red>
        <Option>option 3</Option>
      </Select>
    </div>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043783" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044342" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

*   <font _mstmutation="1" _msthash="464503" _msttexthash="16890276">渲染 和 组件。</font>```App``````Select``````Option```
*   ```Option.Blue```<font _mstmutation="1" _msthash="464880" _msttexthash="21332727">是"颜色组件"。</font>```Option.Red```

**选项.js**

 <code>sdsdimport React, { useEffect } from "react";

function Option(props) {
  const { children, style, value, setStyle } = props;
  useEffect(() => {
    if (setStyle) setStyle({ backgroundColor: style.backgroundColor });
  }, [setStyle, style]);
  return (
    <option value={value} style={style}>
      {children}
    </option>
  );
}

Option.Blue = function (props) {
  props.style.backgroundColor = "blue";
  return Option(props);
};

Option.Red = function (props) {
  props.style.backgroundColor = "red";
  return Option(props);
};
export default Option;</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044758" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045317" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

*   <font _mstmutation="1" _msthash="465439" _msttexthash="326434914">在这里，您可以看到 和 的实现。显而易见，我们渲染组件，只需向道具添加属性。</font>```Option.Blue``````Option.Red``````Option```
*   <font _mstmutation="1" _msthash="465816" _msttexthash="146682796">来自 。它用于将所选颜色更改为所选选项的颜色。</font>```setStyle``````Select```

**选择.js**

 <code>import React, { useState } from "react";

export default function Select(props) {
  const { children } = props;
  const [style, setStyle] = useState({});

  const findOptionActive = (e) => {
    const index = e.target.value * 1;
    const optionStyle = { ...e.nativeEvent.target[index].style };
    if (optionStyle) setStyle({ backgroundColor: optionStyle.backgroundColor });
  };

  const childrenWithProps = React.Children.map(children, (child, index) => {
    return React.cloneElement(child, {
      ...child.props,
      value: index,
      setStyle:
        index === 0 && Object.keys(style).length === 0 ? setStyle : null,
      style: { backgroundColor: "white" }
    });
  });

  return (
    <select onChange={findOptionActive} style={style}>
      {childrenWithProps}
    </select>
  );
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042795" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043354" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

*   <font _mstmutation="1" _msthash="463554" _msttexthash="78841269">现在，我们有一个具有 属性的 select 函数。</font>```onChange``````style```
*   ```findOptionActive```<font _mstmutation="1" _msthash="463931" _msttexthash="122145036">获取选项的样式并相应地更改选择的样式，</font>
*   <font _mstmutation="1" _msthash="464308" _msttexthash="805291435">魔法真的发生在.通常，当收到时，我们无法访问儿童道具 - 但在的帮助下，我们能做到。正如你所看到的，我们可以通过 ， 和 作为道具.</font>```childrenWithProps``````Select``````children``````React.Children``````React.cloneElement``````value``````setStyle``````style```

要获取完整[代码，](https://zshipu.com/t?url=https://codesandbox.io/s/compound-components-xw3b2?file=/src/App.js)请单击此处。

