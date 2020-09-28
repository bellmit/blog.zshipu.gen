
title: CSS样式：CSS 动画
author: 知识铺
date: 2020-09-17 10:06:38
tags: css
---
 # [](#introduction)<font _mstmutation="1" _msthash="288184" _msttexthash="5211505">介绍</font>

**警告**：

这篇文章是为那些从未在CSS中玩过红盒子的人准备的。事实上，这里是红框😁：

[![red box](https://res.cloudinary.com/practicaldev/image/fetch/s--lHxCfcoy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/lb4w44q1eisp5wvmutk1.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--lHxCfcoy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/lb4w44q1eisp5wvmutk1.png)

<font _mstmutation="1" _msthash="276809" _msttexthash="9384167">Html：</font>

 <code><div class="box"></div></code> 

<font _mstmutation="1" _msthash="277381" _msttexthash="8521292">Css：</font>

 <code>.box {
  width: 100px;
  height: 100px;
  background: red;
}</code> 

不用再做，我们开始吧。

# [](#css-transitions)<font _mstmutation="1" _msthash="303160" _msttexthash="8435726">CSS 转换</font>

CSS 中的动画通过**转换和****动画完成**。

转换用于不太复杂的动画，主要是从一**个阶段移动到另一个阶段**- 因此名称。

<font _mstmutation="1" _msthash="290914" _msttexthash="517485748">我们将通过为红色框背景颜色在悬停时从红色到蓝色进行动画处理来学习过渡。首先，我们将添加悬停：</font>

 <code>.box:hover {
  background-color: blue;
}</code> 

没有过渡，我们得到：

[![no transition](https://res.cloudinary.com/practicaldev/image/fetch/s--JUcy8-qP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/cthgum3wrgfqqoyda4nv.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--JUcy8-qP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/cthgum3wrgfqqoyda4nv.gif)
<font _mstmutation="1" _msthash="291811" _msttexthash="67314819">现在，让我们向它添加一个动画。</font>

转换有**4个属性**：转换属性、过渡持续时间、转换-时序函数、过渡延迟。

*   ```transition-property```<font _mstmutation="1" _msthash="464230" _msttexthash="582728315">：采用要添加过渡效果的 CSS 属性的名称，如变换、颜色、宽度。默认**为所有**，这意味着它将动画的所有属性更改。</font>

<font _mstmutation="1" _msthash="292708" _msttexthash="143485004">让我们设置为背景**色，**以检测框的背景颜色变化。</font>```transition-property```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  transition-property: background-color;
}</code> 

<font _mstmutation="1" _msthash="290602" _msttexthash="155103195">若要为多个属性设置动画，请用逗号将它们分开：</font>

 <code>.box{
  /* ... */
  /* animate changes in background-color, color and opacity */
  transition-property: background-color, color, opacity;
}</code> 

<font _mstmutation="1" _msthash="291200" _msttexthash="36517130">或与关键字**全部**：</font>

 <code>.box{
  /* ... */
  /* animate changes to everything */
  transition-property: all;
}</code> 

*   ```transition-duration```<font _mstmutation="1" _msthash="463593" _msttexthash="393239431">：以秒或毫秒为单位的转换持续时间。默认值**为 0s**。因此，我们需要更改它才能运行转换。</font>

<font _mstmutation="1" _msthash="292097" _msttexthash="38151815">让我们在框中添加**一个 2.5s。**</font>```transition-duration```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  transition-property: background-color;
  /* run transition for 2.5s */
  transition-duration: 2.5s;
}</code> 

我们得到这个：

[![transition](https://res.cloudinary.com/practicaldev/image/fetch/s--k_5u1Yln--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9eubwynlbb73mtib8aju.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--k_5u1Yln--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9eubwynlbb73mtib8aju.gif)

*   ```transition-timing-function```<font _mstmutation="1" _msthash="462332" _msttexthash="1765789142">：用于选择要使用的速度曲线类型。默认值为缓**，（**缓慢启动，然后快速，然后慢结束）。也有线性**，****易中，****易出****，轻松**。您还可以使用立方[贝塞尔函数创建](https://zshipu.com/t?url=https://www.w3schools.com/cssref/func_cubic-bezier.asp)自己的函数（但这超出了本教程的范围）。</font>

<font _mstmutation="1" _msthash="290888" _msttexthash="85326605">不同值的比较。让我们为框**设置线性。**</font> ```transition-timing-function```[![timing function](https://res.cloudinary.com/practicaldev/image/fetch/s--GZtz1PpB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/1jwi9kn81d35lxv2daay.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--GZtz1PpB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/1jwi9kn81d35lxv2daay.gif)```transition-timing-function```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  transition-property: background-color;
  /* run transition for 2.5s */
  transition-duration: 2.5s;
  /* set the speed curve to linear */
  transition-timing-function: linear;
}</code> 

*   ```transition-delay```<font _mstmutation="1" _msthash="463268" _msttexthash="93855073">：在开始转换之前添加延迟。默认值为**0s**。</font>

<font _mstmutation="1" _msthash="291785" _msttexthash="26628420">让我们设置一个**2s。**</font>```transition-delay```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  transition-property: background-color;
  /* run transition for 2.5s */
  transition-duration: 2.5s;
  /* set the speed curve to linear */
  transition-timing-function: linear;
  /* add a 2s initial delay */
  transition-delay: 2s;
}</code> 

我们得到这个：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--BGxcc7NJ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/edvsb0jiizxxpsmb9k20.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--BGxcc7NJ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/edvsb0jiizxxpsmb9k20.gif)

总之，我们将 css 属性给**转换属性进行**监视。当检测到这些属性的更改时，将从旧值转换到新值。我们设置它运行多长时间**与过渡持续时间**。我们可以使用过渡定时函数**自定义动画速度曲线，**并添加具有过渡**延迟的延迟**。

<font _mstmutation="1" _msthash="293280" _msttexthash="55363893">这 4 个属性有一个速记： 。</font>```transition```

### [](#the-transition-property)<font _mstmutation="1" _msthash="304603" _msttexthash="11953656">转换属性</font>

**过渡**是过渡属性、**过渡持续时间、****转换定时****函数、**转换**延迟的速**记属性：

过渡：属性持续时间计时功能延迟;

<font _mstmutation="1" _msthash="291772" _msttexthash="27045200">默认值相同：</font>```transition: all 0s ease 0s;```

<font _mstmutation="1" _msthash="292071" _msttexthash="201202508">_注意_： 虽然 默认为**是大多数**开发人员编写**全部**。例如，而不是 。</font>```transition-property``````transition: all 2s;``````transition: 2s;```

<font _mstmutation="1" _msthash="292370" _msttexthash="125213608">通过用替换框的四个_过渡属性_，我们得到：</font>```transition```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  /* run transition for 2.5s */
  /* set the speed curve to linear */
  /* add a 2s initial delay */
  transition: background-color 2.5s linear 2s;
}</code> 

<font _mstmutation="1" _msthash="292968" _msttexthash="393975192">如果我们也想旋转那个盒子呢？
我们可以在悬停时添加旋转效果，让我们添加 180deg 的旋转：</font>

 <code>.box:hover {
  background-color: blue;
  transform: rotate(180deg);
}</code> 

<font _mstmutation="1" _msthash="293566" _msttexthash="47729617">并更改所有转换**属性**：</font>```transition```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  /* run transition for 2.5s */
  /* set the speed curve to linear */
  /* add a 2s initial delay */
  transition: all 2.5s linear 2s;
}</code> 

<font _mstmutation="1" _msthash="291460" _msttexthash="176495202">默认旋转为 0deg，因此转换将检测更改并设置动画：</font>
[![all transition](https://res.cloudinary.com/practicaldev/image/fetch/s--sf63FzuM--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/ubdm2sg3b05l2m4atbn4.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--sf63FzuM--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/ubdm2sg3b05l2m4atbn4.gif)

<font _mstmutation="1" _msthash="291759" _msttexthash="526927765">如果我们想要从 转换不同，我们不能使用**所有**。我们需要添加背景色和转换转换到过渡，用逗号分隔：</font>```background-color``````transform```

 <code>.box{
  /* ... */
  /* animate changes in background-color */
  /* run transition for 2.5s */
  /* set the speed curve to linear */
  /* add a 2s initial delay */
  /* animate changes in transform  */
  /* run transition for 1.5s */
  /* set the speed curve to ease */
  /* add a 4s initial delay */
  transition: background-color 2.5s linear 2s, transform 1.5s ease 4s;
}</code> 

<font _mstmutation="1" _msthash="292357" _msttexthash="19322836">我们得到：</font>
[![different transition](https://res.cloudinary.com/practicaldev/image/fetch/s--OJ2Y916D--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/rp75yfvlqza3m7k686qe.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--OJ2Y916D--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/rp75yfvlqza3m7k686qe.gif)

注意：我们不必指定转换的每个属性。我们可以跳过那些我们不会改变。

例子：

*   ```transition: transform 0.3s;```<font _mstmutation="1" _msthash="586612" _msttexthash="536169309">\> 转换更改的转换转换持续时间为 0.3 秒。默认情况下，转换计时函数设置为简化，并转换延迟设置为 0。</font>

*   ```transition: width 5s 1s;```<font _mstmutation="1" _msthash="586989" _msttexthash="137035730">\> 宽度转换的持续时间为 5 秒，过渡延迟为 1 秒。</font>

*   ```transition: 0.5s;```<font _mstmutation="1" _msthash="587366" _msttexthash="119399774">\> 所有属性的转换在 0.5 秒的持续时间内更改。</font>

*   ```transition: all 1s linear;```<font _mstmutation="1" _msthash="587743" _msttexthash="286618436">\> 所有属性的转换在持续时间为 1 的持续时间更改，计时函数设置为线性。</font>

到我们小介绍过渡到今天。现在，让我们来看看在CSS中设置动画的另一种方式。

# [](#css-animation)<font _mstmutation="1" _msthash="307164" _msttexthash="7066813">CSS 动画</font>

带关键帧的动画更适合复杂动画。
有7个属性：动画名称、动画持续时间、动画定时功能、动画延迟、动画迭代计数、动画方向、动画填充模式。

*   ```animation-name```<font _mstmutation="1" _msthash="463541" _msttexthash="33813468">采用关键帧的名称。</font>

<font _mstmutation="1" _msthash="292045" _msttexthash="203211463">@keyframes是控制动画步骤的 css 规则。
它的基本语法是：</font>

 <code>@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}</code> 

*   ```fadeIn```<font _mstmutation="1" _msthash="585975" _msttexthash="68946670">是一个我们给关键帧的仲裁名称。</font>

*   当动画开始时，此关键帧将为不透明度从 0 动画动画动画结束时的 1 设置动画。

<font _mstmutation="1" _msthash="292942" _msttexthash="94772977">提示： 有些人更喜欢使用从 / 到语法：</font>

 <code>@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}</code> 

以上操作完全相同，从 <> 0% 到 <> 100%。

*   <font _mstmutation="1" _msthash="465725" _msttexthash="56751097">使用关键帧，我们可以：</font>
    *   定义尽可能多的关键帧，我们希望从 0 到 100%。
    *   设置尽可能多的属性的动画。
    *   并且无需在每个关键帧上具有相同的属性。
    *   跳过 0 或 100% - 尽管它不建议因为兼容性问题。

 <code>@keyframes weirdAnim {
  0% { background-color: pink; }
  11% { 
    color: orange;
    padding: 2rem;
  }
  50% { font-size: 1.5rem; }
  66% { transform: rotate(-90deg); }
  99% { background-color: indigo; }
  100% { 
    background-color: orange;
    color: pink;
  }
}</code> 

<font _mstmutation="1" _msthash="291733" _msttexthash="85065175">为我们提供的此关键帧设置动画：</font>
[![weird anim](https://res.cloudinary.com/practicaldev/image/fetch/s--7_s0FhFj--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/md72o5j92ht02vdy6dc0.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--7_s0FhFj--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/md72o5j92ht02vdy6dc0.gif)

<font _mstmutation="1" _msthash="292032" _msttexthash="264451148">我们将为红色盒子的背景颜色设置动画，使之与彩虹的颜色为动画：</font>

 <code>@keyframes rainbow {
  0% { background-color: red; }
  20% { background-color: orange; }
  35% { background-color: yellow; }
  50% { background-color: green; }
  60% { background-color: blue; }
  80% { background-color: indigo; }
  100% { background-color: violet; }
}</code> 

<font _mstmutation="1" _msthash="292630" _msttexthash="320024185">现在，要将此动画添加到我们的框中，我们将添加并将其设置为关键帧的名称：</font>```animation-name```

 <code>.box{
  /* ... */
  animation-name: rainbow;
}</code> 

类似于我们的过渡：

*   ```animation-duration```<font _mstmutation="1" _msthash="465400" _msttexthash="290725214">设置动画的持续时间。默认值为**0s**。让我们将持续时间设置为 5s 到我们的框：</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
}</code> 

*   ```animation-timing-function```<font _mstmutation="1" _msthash="466024" _msttexthash="322717551">设置动画的速度曲线。默认值为"轻松**"。**让我们在框中添加一个缓动的计时功能：</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
  animation-timing-function: ease-in-out;
}</code> 

*   ```animation-delay```<font _mstmutation="1" _msthash="463827" _msttexthash="165615723">设置初始延迟。默认值为**0s**。让我们向框中添加 1s 延迟：</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
  animation-timing-function: ease-in-out;
  animation-delay: 1s;
}</code> 

我们得到：

[![animation](https://res.cloudinary.com/practicaldev/image/fetch/s---k5xq9dx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/98m809bdhh1xhize91s6.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s---k5xq9dx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/98m809bdhh1xhize91s6.gif)

*   请注意，动画结束后，框背景颜色如何跳回红色。

最后三个特定于动画：

*   ```animation-iteration-count```<font _mstmutation="1" _msthash="465699" _msttexthash="719867161">设置我们想要播放动画的时间。默认值为**1**。我们可以通过将此属性设置为无限 来使动画无限期地**运行**。让我们选择运行它 3 次：</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
  animation-timing-function: ease-in-out;
  animation-delay: 1s;
  animation-iteration-count: 3;
}</code> 

*   ```animation-direction```<font _mstmutation="1" _msthash="466323" _msttexthash="216109374">设置我们希望动画播放的方式。值为：**法线**、**反向****、交替****和交替反转**。</font>
    *   <font _mstmutation="1" _msthash="854828" _msttexthash="45635694">**正常**从第一个关键帧开始。</font>
    *   <font _mstmutation="1" _msthash="855348" _msttexthash="49597041">**反向**从最后一个关键帧开始。</font>
    *   <font _mstmutation="1" _msthash="855868" _msttexthash="233085736">**备用**从第一个关键帧开始，但如果重复动画，下一个动画将向后移动。</font>
    *   <font _mstmutation="1" _msthash="856388" _msttexthash="162742853">**备用反向与**备用反向相同，只是它从最后一个关键帧开始。</font>

<font _mstmutation="1" _msthash="294710" _msttexthash="151978450">下面是[w3学校的例子](https://zshipu.com/t?url=https://www.w3schools.com/cssref/playit.asp?filename=playcss_animation-direction)。默认值为**正常**。我们将选择替代。</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
  animation-timing-function: ease-in-out;
  animation-delay: 1s;
  animation-iteration-count: 3;
  animation-direction: alternate;
}</code> 

*   ```animation-fill-mode```<font _mstmutation="1" _msthash="464438" _msttexthash="718306212">指定动画未播放时元素的样式。可以设置为转发**以接受**最后一个关键帧的值。或**向后**采取第一个关键帧的值。或**两者兼而有之**。默认值为**none**。</font>

<font _mstmutation="1" _msthash="292903" _msttexthash="1029931097">提示**：在**动画结束之后，通常会使用转发来保持动画处于最终状态。如果没有它，停止动画化的元素将跳回动画前的状态。
让我们向框动画添加转发填充模式：</font>

 <code>.box{
  /* ... */
  animation-name: rainbow;
  animation-duration: 5s;
  animation-timing-function: ease-in-out;
  animation-delay: 1s;
  animation-iteration-count: 3;
  animation-direction: alternate;
  animation-fill-mode: forwards;
}</code> 

<font _mstmutation="1" _msthash="293501" _msttexthash="29408327">我们得到这个：</font>
[![keyframes final animation](https://res.cloudinary.com/practicaldev/image/fetch/s--8D88ckXr--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/ccztxv7topyabioi3y6y.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--8D88ckXr--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/ccztxv7topyabioi3y6y.gif)

*   在第一个动画中，它从红色开始，以紫色结束。

*   在第二个动画中，它向后运行，因为我们将它设置为备用，因此它从紫色开始，以红色结束。

*   在第 3 个动画中，它再次向后运行，因此从红色开始，以紫色结尾。背景颜色在动画结束后不会跳回红色，因为我们将填充模式设置为前进。

总之，**我们使用@keyframes设置**动画。我们通过在动画名称中引用其名称来引用**该关键帧**。我们设置它运行多长时间**与动画持续时间**。我们可以用动画定时功能**自定义动画速度曲线，**并添加具有动画**延迟的延迟**。

我们还可以指定要使用动画**迭代计数**运行动画次数，更改动画**方向以**选择要通过关键帧**的方向和动画填充模式**，以在动画之后更改动画的元素样式。

<font _mstmutation="1" _msthash="294697" _msttexthash="1271816">There's a shorthand for those 7 properties: .</font>```animation```

### [](#the-animation-property)<font _mstmutation="1" _msthash="308906" _msttexthash="11013236">动画属性</font>

**动画**是动画名称、动画**持续时间**、动画**定**时函数、动画延迟_*、动画迭代_计数_、**动画方向__、**动画填充模式_*的速记属性，按此顺序排列：

动画：名称持续时间时序-函数延迟迭代计数方向填充模式;

<font _mstmutation="1" _msthash="305617" _msttexthash="27045200">默认值相同：</font>```animation: none 0 ease 0 1 normal none;```

<font _mstmutation="1" _msthash="305929" _msttexthash="119122380">通过用框的 7 个动画属性替换，我们得到：</font>```animation```

 <code>.box{
  /* ... */
  animation: rainbow 5s ease-in-out 1s 3 alternate forwards;
}</code> 

就像对于转换一样，我们可以跳过我们不会改变的属性。

例子：

*   ```animation: fadeIn 0.5s;```<font _mstmutation="1" _msthash="610233" _msttexthash="902539105">[> 运行名为 fadein @keyframes 0.5s 的动画。默认情况下，计时函数设置为缓，延迟为 0s，迭代计数为 1，方向正常，填充模式为无。</font>

*   ```animation: grow 2s forwards;```<font _mstmutation="1" _msthash="610623" _msttexthash="248903967">[> @keyframes 2s 增长的动画将填充模式设置为转发以保留最终状态。</font>

*   ```animation: yoyo 0.3s infinite alternate;```<font _mstmutation="1" _msthash="611013" _msttexthash="325315640">[> @keyframes 0.3s 的 10 个动画，迭代计数设置为无限，方向设置为备用。</font>

最后，我们对关键帧动画的介绍很少。

# [](#after-words)<font _mstmutation="1" _msthash="321685" _msttexthash="14023685">之后的话。</font>

*   并不是每个属性都可以进行动画处理。例如，不能对显示从内联更改为块进行动画动画更改。如果有疑问，请检查[此可动画属性的 MDN 列表](https://zshipu.com/t?url=https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)。

*   小心你在动画。这太糟糕了， 但可以玩最新游戏的手机可以滞后于简单的动画🤷 ♀️。**转换****和不透明度在**移动设备上获得 CPU 提升。因此，不要更改字体大小，而是使用转换：缩放（）;而不是更改左、右、上、下使用转换：翻译Y（） 和转换：翻译X（）。


