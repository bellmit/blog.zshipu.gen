
title: JavaScript基础：快速查看 JavaScript 中的 forEach 方法
author: 知识铺
date: 2020-10-19 21:29:30
tags: js
---
forEach 数组方法基本上对_数组中的每一_项执行一些操作。听起来直截了当...

<font _mstmutation="1" _msthash="275951" _msttexthash="364983515">在下面的示例中，我们有 一个 数组。_for 数组_中每个项，_我们控制台_将**项添加到末尾**的项。</font>```goodBoys```

 <code>const goodBoys = ["Spike", "Humphrey", "Snuffles"]

goodBoys.forEach(item => {
  console.log(item + "!")
})
// Spike!
// Humphrey!
// Snuffles!</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1006096" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1006642" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="276523" _msttexthash="221456469">向函数_添加第_二个参数（如下所示）以获取数组中每个项的索引。</font>

 <code>const goodBoys = ["Spike", "Humphrey", "Snuffles"]

goodBoys.forEach((item, index) => {
  console.log(item, index)
})
// Spike 0
// Humphrey 1
// Snuffles 2</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1006720" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1007266" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="277095" _msttexthash="1725716265">请注意，ForEach 不操作数组。它只是允许您对每个项目进行一些处理。在下面的示例中，我创建了一个名为 newArray 的空数组。使用**forEach**循环浏览每个项目，**然后推送（）**将每个项目 \ **！**附加到 newArray 中。</font>

 <code>const goodBoys = ["Spike", "Humphrey", "Snuffles"]
const newArray = []

goodBoys.forEach(item => {
  newArray.push(item + "!")
})
console.log(newArray)
// ['Spike!', 'Humphrey!', 'Sniffles!']</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1007344" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1007890" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>


