
---
title: 完整的入门vue指南
author: 知识铺
date: 2021-01-25 22:39:08+08:00
tags: [vuejs]
---
Vue.js是一个前端框架，针对渐进式集成进行了优化。这意味着您可以拥有一个只集成了几个 Vue 组件的大型应用程序，或者您可以从头开始，在 Vue 生态系统中完全工作。

另一个让 Vue 与众不同的是与很多框架相比，学习曲线较低。如果您了解 HTML、CSS 和 JavaScript，那么您就已经非常接近了， 而不必理解复杂的主题！

与任何框架一样，它向前端添加了结构和实用程序，以便随着应用的增长而更易于扩展，组织更有序，并且不必经常"重新发明轮子"。

Vue也很酷，因为它的生态系统非常集成——很多通常是第三方库的实用程序是由Vue核心维护者建造的，比如[Vue路由器](https://zshipu.com/t?url=https://router.vuejs.org/)[和Vuex。](https://zshipu.com/t?url=https://vuex.vuejs.org/)

在这篇文章中，我们将探讨Vue的主要功能，并一起创建一个应用程序！

下面是我们将构建的，不过具有一些更交互的功能。"喜欢"按钮会根据用户点击从心脏轮廓切换到红心。此外，当有人在文本框中输入时，字符号将倒计时。

继续查看上面的 HTML 和 CSS 代码，我们将使用 Vue 代码构建 HTML。

## [](#setting-up-a-vue-app)<font _mstmutation="1" _msthash="290849" _msttexthash="25940148">设置 Vue 应用程序</font>

现在，我们将使用Vue CDN ——我们想要一个极简的设置。将来，您可能需要一个更广泛的环境，在这种情况下，您可以使用[Vue CLI](https://zshipu.com/t?url=https://cli.vuejs.org/)。

<font _mstmutation="1" _msthash="290316" _msttexthash="1058130801">转到"Codepen"上的按钮，切换到 JavaScript 选项卡，并在 CDNjs 上搜索 Vue。这会将 Vue 库添加到我们的项目中，因此我们可以使用 Vue 提供的所有方法和功能。</font>```settings```

现在，我们需要创建一个 Vue 实例并将其附加到我们的 HTML，以便完全集成 Vue！

<font _mstmutation="1" _msthash="290914" _msttexthash="60137532">让我们创建一个存储实例的实例。</font>```const``````Vue```

 <code>const app = new Vue()</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042522" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043081" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

我们将传递一个对象，当我们创建这个Vue应用程序，它将有我们所有的配置和应用程序逻辑现在。

<font _mstmutation="1" _msthash="291811" _msttexthash="611637468">我们要添加到该对象的第一件事是 - 这是我们想要成为我们的 Vue 应用程序的基础的元素。在这种情况下，具有 类的元素。</font>```el``````status```

 <code>const app = new Vue({
  el: ".status"
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043497" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044056" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292409" _msttexthash="1724486790">然后，我们将添加我们的 。为了测试这一点，让我们添加作为数据——因此，我们现在拥有的地方将成为一个变量。在路上， 我们将用不同的文本制作更多的推文， 所以让推文的这一部分成为动态的是有道理的。</font>```data``````tweetText``````Hello World!```

 <code>const app = new Vue({
    el: ".status",
    data: {
        tweetText: "Hello World!"
    }
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044147" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044706" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="290303" _msttexthash="460451550">当我们想要添加更多的动态数据（或将在 Vue 应用中更改的数据）时，我们将向此对象添加更多属性。</font>```data```

现在，我们可以在 HTML 中使用新创建的数据，然后这样插入变量！如果你曾经使用过把手或其他模板语言， 它有点像。

<font _mstmutation="1" _msthash="290901" _msttexthash="77213942">如果您转到 HTML 中的硬编码"Hello World！"</font>```{{tweetText}}```

 <code><p class="tweet-text">
  {{ tweetText }}
</p></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042509" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043068" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291499" _msttexthash="131966406">尝试在 Vue 中更改您的，它会改变您的输出！</font>```tweetText```

让我们集思广益，了解一下我们在应用过程中将发生哪些其他数据。

*   心在喜欢和与众不同之间切换
*   当我们键入

<font _mstmutation="1" _msthash="292396" _msttexthash="81564509">让我们继续为对象中的属性添加属性。</font>```data```

 <code>data: {
    tweetText: "Hello World!",
+    charactersRemaining: 280,
+    liked: false }</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044134" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044693" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292994" _msttexthash="42365830">我们还在 HTML 中动态显示。</font>```charactersRemaining```

 <code><span class="characters-remaining">
  {{ charactersRemaining }} characters remaining
</span></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1041846" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1042405" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="290888" _msttexthash="126657492">我们将保留属性现在， 我们将在一秒钟后回到它。</font>```liked```

## [](#methods)<font _mstmutation="1" _msthash="304655" _msttexthash="5267275">方法</font>

现在，我们已经拥有了数据，我们需要根据用户操作进行更新。

<font _mstmutation="1" _msthash="291785" _msttexthash="169260351">我们将向 Vue 对象添加另一个属性 - 此属性将存储我们的方法。</font>

 <code>const app = new Vue({
    el: ".status",
    data: {
        tweetText: "Hello World!",
        charactersRemaining: 280,
        liked: false
    },
    methods: {}
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043471" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044030" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

我们的应用有两个"操作"，在用户设置时切换等字符并更改剩余字符数。让我们先处理字符计数。

<font _mstmutation="1" _msthash="292682" _msttexthash="94113877">我们将首先向方法对象添加一个函数：</font>

 <code>methods: {
    countCharacters: function() {

    }
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044446" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045005" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293280" _msttexthash="769950038">让我们考虑一下此函数的逻辑：我们需要计算用户在 中键入的字符数。然后，我们需要从 280（或我们的字符限制）中减去该计数。</font>```textarea```

<font _mstmutation="1" _msthash="290875" _msttexthash="286559013">让我们为注释文本创建一个数据属性，然后在 每次用户在 中输入时更新该属性。</font>```textarea```

  <code>data: {
    tweetText: 'Hello World!',
    charactersRemaining: 280,
+    commentText: '',
    liked: false
  },</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042483" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043042" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

 <code><textarea placeholder="tweet your reply" v-model="commentText"></textarea></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042808" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043367" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

```v-model```<font _mstmutation="1" _msthash="291772" _msttexthash="1090536369">是_一个_指令，它将数据属性与用户键入到 的内容同步。因此，无论他们键入多少或很少，将匹配他们键入。要快速退一步_，指令_是由 Vue 提供的 HTML 属性，它们由 前缀。</font>```textarea``````commentText``````v-```

<font _mstmutation="1" _msthash="292071" _msttexthash="483780635">好了，现在回到我们的方法。我们可以使用 （以下是 JavaScript 的[](https://zshipu.com/t?url=https://codeburst.io/all-about-this-and-new-keywords-in-javascript-38039f71780c)很好参考 ） 来访问我们的方法中的数据。</font>```this.myDataAttribute``````this```

<font _mstmutation="1" _msthash="292370" _msttexthash="93963701">因此，我们可以使用以下逻辑更新 ：</font>```charactersRemaining```

 <code>methods: {
    countCharacters: function() {
        this.charactersRemaining = 280 - this.commentText.length
    }
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044108" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044667" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292968" _msttexthash="129637768">现在，我们需要确保每次用户在 中输入 时运行 。</font>```countCharacters``````textarea```

<font _mstmutation="1" _msthash="293267" _msttexthash="1008139704">幸运的是，Vue 具有指令，我们可以在它之后添加事件，以便我们每次发生该事件时都运行该方法。在这种情况下，将在每次用户在 中输入 时运行 该方法。</font>```v-on``````v-on:input="countCharacters"``````countCharacters``````textarea```

 <code><textarea
  placeholder="tweet your reply"
  v-model="commentText"
  v-on:input="countCharacters"
></textarea></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1045083" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045642" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291161" _msttexthash="147794790">好了，现在让我们退后一步，研究一下我们的方法。</font>```toggleLike```

<font _mstmutation="1" _msthash="291460" _msttexthash="85782164">我们首先需要将该方法添加到对象中。</font>```methods```

 <code>methods: {
    ...
    toggleLike: function () {

    }
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043120" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043679" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292058" _msttexthash="97502964">方法的正文应更改为与当前相反。所以：</font>```this.liked```

 <code>toggleLike: function () {
    this.liked = !this.liked
}</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043770" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044329" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

现在我们需要运行该操作。

<font _mstmutation="1" _msthash="292955" _msttexthash="83724108">在 div 上，让我们添加一个事件侦听器。</font>```reactions```

 <code><div class="reactions like" v-on:click="toggleLike">
  ...
</div></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044745" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045304" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

是时候引入另一个 Vue 功能了： 条件！

## [](#conditionals)<font _mstmutation="1" _msthash="307437" _msttexthash="4510571">条件</font>

<font _mstmutation="1" _msthash="291447" _msttexthash="94109574">Vue 允许我们有条件地使用指令呈现数据。</font>```v-if```

<font _mstmutation="1" _msthash="291746" _msttexthash="102324521">让我们在 div 中添加以下跨包表情符号：</font>```reactions```

 <code><span v-if="liked">♥️</span></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043432" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043991" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292344" _msttexthash="564041465">现在，我们的红心表情符号只出现，如果是。让我们也添加一个到我们的心脏轮廓表情符号，以便它只呈现如果 是 。</font>```liked``````true``````v-else``````liked``````false```

 <code><span v-if="liked">♥️</span> <span v-else>♡</span></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044082" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044641" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

耶！现在我们喜欢工作！

如果您对上述步骤有任何问题，下面是一个包含我们到目前为止所拥有内容的 Codepen。

现在，我们的交互已降低，我们如何创建一堆具有相同功能但数据不同的推文？组件！

## [](#components)<font _mstmutation="1" _msthash="307736" _msttexthash="5055388">组件</font>

与其他前端框架类似，Vue 应用程序被分解为组件。我们组合组件以创建完整的用户界面。一个很好的经验法则是，如果用户界面的一个块被多次使用，它应该被分解为一个组件。

在生产应用程序中，我们的推文可能会被分解为子组件 ——我们可能有一个注释文本区域的组件，一个用于"喜欢的功能"，一个用于个人资料图片的组件，等等。但是， 现在， 我们将只是把完整的推文变成一个组件， 以便我们可以轻松地创建一堆更多的推文。

首先，让我们将逻辑从 Vue 实例移动到一个组件中。

<font _mstmutation="1" _msthash="292630" _msttexthash="855845744">的第一个参数是组件的名称，本例中为"tweet"。我们还将数据转换为返回对象的函数。这允许我们有多个组件实例，每个实例都有单独的数据。</font>```Vue.component``````tweet```

 <code>Vue.component("tweet", {
  data: function() {
    return {
      charactersRemaining: 280,
      commentText: "",
      liked: false
    }
  },
  methods: {
    countCharacters: function() {
      this.charactersRemaining = 280 - this.commentText.length
    },
    toggleLike: function() {
      this.liked = !this.liked
    }
  }
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044394" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044953" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293228" _msttexthash="412546251">我们还需要 组件的 - 或组件将呈现的 HTML。我们将获取所有现有的 HTML 并粘贴到组件上的模板属性中。</font>```template```

 <code>template: `<div class="status">
  <div class="tweet-content">
    <img src="https://pbs.twimg.com/profile_images/1070775214370373633/borvu2Xx_400x400.jpg" class="logo" alt="Vue Vixens DC logo">
    <div class="tweet">
      <a href="https://twitter.com/vuevixensdc">Vue Vixens DC</a>
      <span>@VueVixensDC · Mar 20</span>
      <p class="tweet-text">
        {{ tweetText }}
      </p>
      <div class="reactions">
        <span v-on:click="toggleLike" class="like">
          <span v-if="liked">♥️</span>
          <span v-else>♡</span>
        </span>
      </div>
    </div>
  </div>
  <div class="comment-bar">
    <textarea placeholder="tweet your reply" v-model="commentText" v-on:input="countCharacters">
    </textarea>
    <span class="characters-remaining">
      {{ charactersRemaining }} characters remaining
    </span>
  </div>
</div>`</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1045044" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045603" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

现在，我们有一个Vue组件！

<font _mstmutation="1" _msthash="294125" _msttexthash="1760846542">我们需要添加的另一个快速的事情： 推文文本将不同于推文到推文。我们将通过传递每个单独推文的不同推文文本 ， 这使我们能够将数据从该组件外部传递到组件。现在，我们将指定我们的组件具有与之关联的道具。</font>```props```

 <code>Vue.component('tweet', {
  props: ['tweetText'],
...
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1046019" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1046578" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292019" _msttexthash="292728215">不过， 我们仍然需要有一个 Vue 应用程序， 所以让我们把它添加回我们的 Javascript：</font>

 <code>new Vue({ el: "#app" })</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043731" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044290" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292617" _msttexthash="904611162">酷， 现在我们的 JavaScript 已设置， 我们只需要处理我们的 HTML 。在我们的 Vue 实例中，我们现在正在寻找一个包含 ID 的元素，因此让我们创建它。</font>```app```

 <code><div id="app"></div></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044381" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044940" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293215" _msttexthash="225239781">而且，在我们的新 Vue 应用程序中，我们将添加一些推文组件的实例。</font>

 <code><div id="app">
  <tweet tweet-text="hello world!"></tweet>
  <tweet tweet-text="hi!"></tweet>
</div></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1045031" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045590" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293813" _msttexthash="821616016">请注意，我们如何传递我们的道具 - Vue 将 JavaScript 骆驼案例转换为 HTML 中的烤肉串案例。除了这种变化之外，我们的道具看起来像 HTML 属性。</font>```tweetText```

现在我们的组件应该很好去！

不过，还有一件快速的事情，通常是在 HTML 中对每条推文进行硬编码，而是要循环浏览数据结构，并为每个项创建一个推文组件。让我们看看如何在 Vue 中做到这一点！

<font _mstmutation="1" _msthash="292305" _msttexthash="152686092">我们将进入我们的 Vue 应用程序实例并添加一些推文数据。</font>

 <code>new Vue({
  el: "#app",
  data: {
    tweets: [
        { id: 1, tweetText: "hello world!" }, 
        { id: 2, tweetText: "hi!" }
    ]
  }
})</code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044043" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044602" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292903" _msttexthash="356889689">现在，我们将使用另一个 Vue 指令，以便循环浏览推文数组，并为每个创建一个实例！</font>```v-for``````tweet```

 <code><div id="app">
  <tweet
    v-for="tweet in tweets"
    v-bind:key="tweet.id"
    v-bind:tweet-text="tweet.tweetText"
  ></tweet>
</div></code> 

 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044694" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="highlight-action highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045252" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293501" _msttexthash="1157713986">请注意，我们在这里使用两次 - 它允许我们动态更新 html 属性（或使用其中中的变量）。每当您使用键时，都会建议使用键 -- 它允许 Vue 更好地识别子元素（[更多](https://zshipu.com/t?url=https://vuejs.org/v2/guide/list.html#key)）。</font>```v-bind``````v-for```

<font _mstmutation="1" _msthash="293800" _msttexthash="195773240">棒！现在，我们可以通过向数组添加元素来创建更多推文！</font>```tweets```

