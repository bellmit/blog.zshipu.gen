
title: React技术：创建炫酷的下落菜单 第二部分
author: 知识铺
date: 2020-09-28 22:19:53
tags: 
---
 [Andrew Bone](https://zshipu.com/t?url=https://dev.to/link2twenty)指出，"一般来说，在制作组件时，目标是使其可重复使用且足够简单，因此很少需要重新访问。

我心上是心底的在下面的，我试图重构我的下拉菜单只是这个：可重用和简单。

[![demo gif](https://res.cloudinary.com/practicaldev/image/fetch/s--pgEiHObr--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/jazget07eufuccrhth7u.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--pgEiHObr--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/jazget07eufuccrhth7u.gif)

> [跳转到 Github 上的代码](https://zshipu.com/t?url=https://github.com/cooljasonmelton/dropdown2)

# [](#tutorial)<font _mstmutation="1" _msthash="289978" _msttexthash="5610267">教程</font>

目标：取上一个下拉菜单并重写代码，以便它可以使用可互换 JSON 对象的数据创建与原始对象具有相同结构和样式的下拉列表。

### [](#table-of-contents)<font _mstmutation="1" _msthash="291122" _msttexthash="5308706">目录</font>

*   初步垃圾
*   映射 JSON 对象
*   动态样式
*   动态路由
*   结论

### [](#preliminary-junk)<font _mstmutation="1" _msthash="304018" _msttexthash="10296754">初步垃圾</font>

首先，我[复制了原始存储库，并创建了一](https://zshipu.com/t?url=https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)个包含一些虚拟数据的 JSON 文件。

[![json file](https://res.cloudinary.com/practicaldev/image/fetch/s--5gMLqz3t--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/sxxfb2bk4yyvgty3yzcc.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--5gMLqz3t--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/sxxfb2bk4yyvgty3yzcc.png)

### [](#mapping-a-json-object)<font _mstmutation="1" _msthash="304954" _msttexthash="15391480">映射 JSON 对象</font>

<font _mstmutation="1" _msthash="291512" _msttexthash="844148799">若要使组件具有动态性，我使用 。映射在 React 应用中很常见，因为它可以将无限大小的数组转换为 JSX。这抽象了组件，使它们灵活且可重用。</font>```map()```

<font _mstmutation="1" _msthash="291811" _msttexthash="60042138">原始组件的返回如下所示：</font>```Menu```

  <code>return (
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
  );</code> 

<font _mstmutation="1" _msthash="292409" _msttexthash="713595181">您可以看到，每个项目都用它自己的 div 和属性进行拼写。在重构版本中，我定义一个 Cookie 刀具菜单项，以及从 JSON 到的每个菜单项。</font>```map()```

<font _mstmutation="1" _msthash="292708" _msttexthash="41750124">新的返回如下所示：</font>

  <code>return (
        <div className="Menu">
            <div className={"m-item m-logo"}
                onClick={() => setOpenMenu(!openMenu)}>
                Menu
            </div>

            {renderMenuItems(data)}

        </div>
  );</code> 

第一个菜单项保留在它自己的 div 中。此项目的作用就像打开下拉列表的按钮。当菜单关闭，其他菜单项隐藏在菜单后面时，它会显示它。

<font _mstmutation="1" _msthash="290901" _msttexthash="115612068">在此下面，我调用以 JSON 对象作为参数的函数。</font>```renderMenuItems()```

```renderMenuItems()```<font _mstmutation="1" _msthash="291200" _msttexthash="162067178">是复杂的。我将显示整个功能，然后一块一块地解释它。</font>

  <code>// render each menu item after Menu button clicked
    const renderMenuItems = data => {    
        const colorArr = ["#9b5de5", "#f15bb5", "#00BBF9"];

        let colorCounter = -1;
        return data.menu.map((item, index) => {

            // if counter is over 2, resets to 0
            // for colorArr bracket notation to get sequence of colors
            colorCounter < 2 ? colorCounter++ : colorCounter = 0

            // dynamic styles for each menu item 
            const itemStyle = {
                "top": `${index * 1.8}em`,
                "backgroundColor": colorArr[colorCounter]
            }

            return (
                <div className="m-item"
                    key={item.id}
                    style={openMenu ? itemStyle : null}
                    onClick={() => pushToRoute(item.route)}>
                    {item.name}
                </div>
            )
        })
    }</code> 

<font _mstmutation="1" _msthash="291798" _msttexthash="93188238">我将解释 ，并在下一节中介绍动态样式。</font>```colorArr``````colorCounter``````itemStyle```

<font _mstmutation="1" _msthash="292097" _msttexthash="53339195">首先，请注意以下行：</font>

  <code>return data.menu.map((item, index) => {</code> 

<font _mstmutation="1" _msthash="292695" _msttexthash="357945003">我返回的 JSON 对象参数。 对数组中的每个项运行回调，返回新数组中该函数的结果。</font>```map()``````data``````map()```

```map()```<font _mstmutation="1" _msthash="292994" _msttexthash="438286459">可以采取两个参数。第一个参数是数组中的项。我贴上了标签。第二个是每个项目的索引，标记为 。</font>```item``````index```

<font _mstmutation="1" _msthash="290589" _msttexthash="27336959">现在这部分：</font>

  <code>return (
                <div className="m-item"
                    key={item.id}
                    style={openMenu ? itemStyle : null}
                    onClick={() => pushToRoute(item.route)}>
                    {item.name}
                </div>
            )</code> 

<font _mstmutation="1" _msthash="291187" _msttexthash="272742106">我返回 中每个项目的动态 JSX。这些将是我们菜单项的 div。每个项目都有 和 和 。</font>```map()``````id``````name``````route```

<font _mstmutation="1" _msthash="291486" _msttexthash="1176365437">我给每个 div 的类名， 与原来的不一样。他们得到一个触发的事件。与原始参数相同，参数在 JSON 对象中作为。每个都得到一个JSON的钥匙。最后，我在 div 中将 JSON 对象的显示为文本。</font>```m-item``````onClick``````pushToRoute()``````route``````id``````name```

<font _mstmutation="1" _msthash="291785" _msttexthash="88011209">作为参考，以下是 JSON 菜单项之一：</font>

  <code>{  "id":  "001",  "name":  "Dashboard",  "route":  "/dashboard"  }</code> 

### [](#dynamic-styles)<font _mstmutation="1" _msthash="306176" _msttexthash="10766561">动态样式</font>

<font _mstmutation="1" _msthash="292682" _msttexthash="1033908759">CSS 负责下拉动画和样式。在我的原始菜单中，我使用调用的函数向项目添加类名。然后，我拼出每个项目的单个类名，包括我想每个项目的颜色和长度。</font>```setClassNames()```

<font _mstmutation="1" _msthash="292981" _msttexthash="48536228">添加类名以触发转换：</font>

  <code>// parameter num corresponds to .open-# classes
    // is assigned when Menu clicked triggering animated dropdown
    const setClassNames = num => {
        const classArr = ["m-item"];
        if (openMenu) classArr.push(`open-${num}`)
        return classArr.join('  ')
    }</code> 

<font _mstmutation="1" _msthash="290875" _msttexthash="25719070">添加的类名：</font>

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

<font _mstmutation="1" _msthash="291473" _msttexthash="583571378">虽然这工作，它是不容易重用。我不仅必须手动拼出每个附加项目的每一个新代码，我还使用了很多额外的代码行。</font>```open-#```

<font _mstmutation="1" _msthash="291772" _msttexthash="290231617">由于我在新的菜单项上使用，我可以一起设计样式。我需要包括两个部分：</font>```map()```

1.  <font _mstmutation="1" _msthash="462319" _msttexthash="144005329">设置为列表中编号项（1.8、3.6、5.4、7.2 等）的大小。</font>```top``````1.8em```
2.  <font _mstmutation="1" _msthash="462696" _msttexthash="131174303">三种颜色十六进制之一设置为 （#9b5de5、#f15bb5、#00BBF9）。</font>```background-color```

<font _mstmutation="1" _msthash="292370" _msttexthash="24040796">请看一次渲染MenuItem。</font>

  <code>// render each menu item after initial Menu button
    const renderMenuItems = data => {    
        const colorArr = ["#9b5de5", "#f15bb5", "#00BBF9"];

        let colorCounter = -1;
        return data.menu.map((item, index) => {

            // if counter is over 2, resets to 0
            // for colorArr bracket notation to get sequence of colors
            colorCounter < 2 ? colorCounter++ : colorCounter = 0

            // dynamic styles for each menu item 
            const itemStyle = {
                "top": `${index * 1.8}em`,
                "backgroundColor": colorArr[colorCounter]
            }

            return (
                <div className="m-item"
                    key={item.id}
                    style={openMenu ? itemStyle : null}
                    onClick={() => pushToRoute(item.route)}>
                    {item.name}
                </div>
            )
        })
    }</code> 

React 允许您将样式作为对象添加到元素中，该对象的属性以 JavaScript 的 camelcase 语法编写。

<font _mstmutation="1" _msthash="293267" _msttexthash="305586710">请注意，我在 中设置了大小。在通过 JSON 进行时，我使用索引参数动态增加 em 大小。</font>```itemStyle``````top``````map()``````map()```

<font _mstmutation="1" _msthash="293566" _msttexthash="672152806">有点棘手。我设置了一个数组，称为 3 个颜色十六进制。为了访问这些，我设置了一个计数器，调用我用于访问十六进制。</font>```background-color``````colorArr``````colorCounter```

<font _mstmutation="1" _msthash="291161" _msttexthash="237597932">最初设置为 -1。为了连续迭代 0、1 和 2 直到完成，我编码了此三元：</font>```colorCounter``````map()```

  <code>// if counter is over 2, resets to 0
            // for colorArr bracket notation to get sequence of colors
            colorCounter < 2 ? colorCounter++ : colorCounter = 0</code> 

如果计数器小于 2，我添加 1。如果超过 2，我重置计数器为 0。因此，计数器将运行 0， 1， 2， 0， 1， 2...只要地图（）去。

<font _mstmutation="1" _msthash="292058" _msttexthash="217985937">在 中，我设置为 colorArr [colorCounter]。因此，颜色出现在序列中。</font>```itemStyle``````“backgroundColor”```

<font _mstmutation="1" _msthash="292357" _msttexthash="161175586">最后，我需要在单击第一个菜单项时才向项添加 和 属性。</font>```top``````background-color```

<font _mstmutation="1" _msthash="292656" _msttexthash="221922649">如前所述，单击时，顶部菜单项在真和假之间切换，一个挂钩。</font>```openMenu``````useState```

<font _mstmutation="1" _msthash="292955" _msttexthash="58598774">我给每个 div 一个样式属性：</font>

  <code>style={openMenu ? itemStyle : null}</code> 

<font _mstmutation="1" _msthash="293553" _msttexthash="261635426">我使用三元在这里返回包含新的和 如果为 true 的对象。如果为 false，它将接收 。</font>```top``````background-color``````openMenu``````null```

### [](#dynamic-routes)<font _mstmutation="1" _msthash="307710" _msttexthash="12632893">动态路由</font>

<font _mstmutation="1" _msthash="291447" _msttexthash="136178523">最后一部分是回到我的语句中，并动态呈现路由。</font>```Switch``````App.js```

<font _mstmutation="1" _msthash="291746" _msttexthash="156569634">我可以使用相同的JSON对象来设置每个菜单项的相应。</font>```map()``````route```

 <code>const App = () => {
  return (
    <BrowserRouter>
      <div className="App">
        {/* dropdown menu */}
        <Menu/>
        {/* routes */}
        <Switch>
          {/* map same data as dropdown to 
            create route for each item */}
          {data.menu.map(item =>{
            return(
              <Route key={item.id}
                exact path={item.route} 
                component={null} />
            )
          })}
        </Switch>
      </div>
    </BrowserRouter>
  );
}</code> 

同样，我错过了此菜单将应用于的应用程序的实际组件。如果它们可用，我可以更改 JSON 以包括组件名称，或者设置一个与 JSON 中的 ID 对应组件的查找表。

