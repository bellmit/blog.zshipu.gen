
---
title: 样式中的 Web 组件
author: 知识铺
date: 2021-03-10 11:53:44+08:00
tags: []
---
Web 组件非常易于样式。您可以以接近零的成本在它们之间共享样式，并且它们仍然可以从外部进行样式设计。它们易于设置和逐步增强。有一大堆使用 Web 组件的框架，如果你进入其中，你自然会知道这一切。但它真的很难理解来自React，Vue，角度等。因此，让我们来谈谈它。

### [](#baseline)<font _mstmutation="1" _msthash="289029" _msttexthash="5423990">基线</font>

网络组件可能是目前网络上最被误解的技术。这真的不是任何人的错，技术是在一个尴尬的地方。这个行业陷入了React热的梦想， 如果不是React， 那么肯定 Vue， 如果不是 Vue， 那么我猜角度？所有这些框架都在它们自己的生态系统中发挥作用。而且很难看出他们之外发生了什么。

Web 组件旨在将每个人带出封闭系统，相互共享。在科技领域制作自己的围墙花园真的很容易，事实上，一旦你创造了它，你就会有动力让它继续下去。要制定每个人都能达成一致的标准并建立互操作性，难度更大。

因此，让我们来看看什么是网络组件字面上。我不得不深入， 因为那里的误解。有三个主要的浏览器功能统称为"Web 组件"：

### [](#custom-elements)<font _mstmutation="1" _msthash="290225" _msttexthash="15095041">自定义元素</font>

<font _mstmutation="1" _msthash="277381" _msttexthash="707135819">能够制作自己的元素，你自己的按钮，你自己的输入什么。实现是愚蠢的简单。您只需创建一个扩展HTMLElement的新类，然后注册名称。</font>

 <code>class MyButton extends HTMLElement {
   connectedCallback() {
       super.connectedCallback();
       console.debug("I just appeared on the page!");
   }
}

customElements.register('my-button', MyButton);</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1007656" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1008202" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="277953" _msttexthash="2044033121">您可以在HTML的任何地方使用。酷。顺便说一句，你可以使用它在React和Vue也。它只是工作。是的，我们必须运行 JavaScript，但很容易逐步增强这一点，因为浏览器对待它就像一个DIV，直到javascript加载。你仍然可以从外面设计它。</font>```<my-button>```

<font _mstmutation="1" _msthash="290017" _msttexthash="2164733844">这种组件的实现是关于你能想到的最简单、最简单的事情。它非常快，因为它已经在使用浏览器的原生对象系统，而且功能完全齐全。此外，当你在浏览器中检查它时，你会看到它，不是一些奇怪的，不是一堆难以辨认的元素。只是。</font>```<div class="rg84823">``````<my-button>```

### [](#html-templates)<font _mstmutation="1" _msthash="304018" _msttexthash="8052564">HTML 模板</font>

HTML 模板是定义 DOM 中的 HTML 片段的一种方式，而无需在页面上实际运行。这可以让你做声明性的事情，而不必使用Java脚本。

### [](#shadow-dom)<font _mstmutation="1" _msthash="304642" _msttexthash="11696594">阴影多姆</font>

<font _mstmutation="1" _msthash="291213" _msttexthash="1635709660">阴影 DOM 是封装和隐藏 HTML 块的一种方式。即使看起来像一个单一的元素，它可以有很多子元素在其阴影DOM。就像元素有它自己无法访问的子元素，如下拉箭头，你的自定义元素可以有自己的小世界。</font>```<my-button>``````<select>```

是的，这有点令人费解。因为你已经习惯了 DOM 树， 以及一棵树。影子多姆把它变成一棵超级树。Node可以在主树上有自己的子树。这有代价， 精神上。而且，老实说，任何优秀的开发人员自然会想在这里关闭他们的大脑，因为复杂性似乎没有立即的回报。但是，与其完全放弃 Web 组件的概念，不如首先记住，我们不必使用 Shadow DOM 来使用自定义元素：其次，也许我们可以继续徒步穿越概念山，看看另一边是什么。

您首先会发现一件事是，它允许您控制 CSS 如何影响组件的内部工作。这允许您保护它免受上面的混乱。具体来说，组件成为级联的边界，或者换句话说，组件的 CSS 将范围确定为它。

<font _mstmutation="1" _msthash="292110" _msttexthash="1744950766">有多种方法可以穿孔和控制组件中的样式。最简单的是，当您编写组件时，需要共享样式。这是一组组件都依赖的CSS样式，一个样式库。浏览器缓存它，但将其赋予每个组件。在照明中，你会做类似的事情：</font>

 <code>const buttonStyles = css`
  .icon { width: 32px; vertical-align: middle }
`;

class MyButton extends LitElement {
  static styles = [buttonStyles, myStyles];
}

class YourButton extends LitElement {
  static styles = [buttonStyles, yourStyles];
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043822" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044381" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292708" _msttexthash="363784408">我的按钮和你的按钮都将使用， 和任何其他他们想要的， 而不会被来自他们上面的 Css 改变。</font>```buttonStyles```

<font _mstmutation="1" _msthash="290303" _msttexthash="1056938259">另一个是CSS变量，如果你不使用，你真的应该。组件在树上从上面获取 CSS 变量。这是常见的定义和发布与您的组件变量，他们支持喜欢。从上面改变它变得简单。</font>```--my-button-color```

我们还拥有 CSS 零件，它允许组件作者定义要更改的部件。

最后，因为它是一个简单的JavaScript类，你可以扩展任何你想要的元素，并交给它新的风格。

有了这些系统，您就会发现CSS更容易管理。与布局、实用程序、页面元素等相比，您自然而然地倾向于单独的造型组件。你会发现你没有筑巢几乎一样多。一般来说，你会发现组织你的样式要容易得多。我甚至不再用 sass / scs 了， 因为我就是不需要它。

### [](#frameworks)<font _mstmutation="1" _msthash="305253" _msttexthash="5190354">框架</font>

让我们来谈谈真正的大误解。人们似乎认为 Web 组件是响应、Vue、角等框架的竞争对手。不！Web 组件为这些框架构建路径，为您提供组件。理想情况下，作为最终开发人员，您永远不必担心自定义元素或 ShadowDOM，除非了解造型和封装的一些细节。

很多框架都在这样做，但不是流行的三巨头，他们每个人都有既得利益，让自己关闭。[看看许多方法，使网络组成](https://zshipu.com/t?url=https://webcomponents.dev/blog/all-the-ways-to-make-a-web-component/)，所有这些框架有不同的策略和系统，但所有这些都可以在任何地方使用，不仅在自己的花园。

是的，您可以以零依赖的方式使用 Web 组件，对于日期选择器或非常具体的一次性内容，这是一个绝佳的选择。但这不是你应该消费甚至创建 Web 组件的主要方式。这只是不断扩大的开放系统中的众多选项之一。

