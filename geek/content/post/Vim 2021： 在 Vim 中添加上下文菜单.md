
---
title: Vim 2021： 在 Vim 中添加上下文菜单
author: 知识铺
date: 2021-03-05 09:00:58+08:00
tags: []
---
当您与光标下的当前单词/行有关时，漂亮的上下文菜单非常有用。它还可以提醒你，当你忘记你的键盘图：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--t7761-0z--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/zd5op8x68wv9k8gh7n5b.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--t7761-0z--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/zd5op8x68wv9k8gh7n5b.gif)

## [](#setup)<font _mstmutation="1" _msthash="289055" _msttexthash="6648122">设置</font>

<font _mstmutation="1" _msthash="276523" _msttexthash="174204264">在ui扩展插件[quickui](https://zshipu.com/t?url=https://github.com/skywind3000/vim-quickui)的帮助下，它可以简单地定义为：</font>

 <code>Plug 'skywind3000/vim-quickui'

" define your context menu as a list of (text, command) pairs
let g:context_menu_k = [
 \ ["&Help Keyword\t\\ch", 'echo expand("<cword>")' ],
 \ ["&Signature\t\\cs", 'echo 101'],
 \ ['-'],
 \ ["Find in &File\t\\cx", 'exec "/" . expand("<cword>")' ],
 \ ["Find in &Project\t\\cp", 'exec "vimgrep " . expand("<cword>") . "*"' ],
 \ ["Find in &Defintion\t\\cd", 'YcmCompleter GotoDefinition' ],
 \ ["Search &References\t\\cr", 'YcmCompleter GoToReferences'],
 \ ['-'],
 \ ["&Documentation\t\\cm", 'exec "PyDoc " . expand("<cword>")'],
 \ ]

" map 'K' to display the context menu
nnoremap <silent>K :call quickui#tools#clever_context('k', g:context_menu_k, {})<cr></code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1006720" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1007266" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="277095" _msttexthash="120906188">然后，当您按下时，它会显示在光标周围：</font>```K```

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--l5gzKXuw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://skywind3000.github.io/images/p/quickui/context.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--l5gzKXuw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://skywind3000.github.io/images/p/quickui/context.png)

上下文菜单是组织 LSP 命令的好地方。

## [](#usage)<font _mstmutation="1" _msthash="290849" _msttexthash="4971109">使用</font>

*   <font _mstmutation="1" _msthash="461734" _msttexthash="53505582">通过/或箭头键导航项目。</font>```j``````k```
*   <font _mstmutation="1" _msthash="462111" _msttexthash="77009894">接受通过或鼠标左键单击的项目。</font>```Enter``````Space```
*   <font _mstmutation="1" _msthash="462488" _msttexthash="10194041">按退出。</font>```ESC```
*   <font _mstmutation="1" _msthash="462865" _msttexthash="16063489">热键可以由 a . .</font>```&```

边框和颜色也是可定制的，请查看 quickui[文档](https://zshipu.com/t?url=https://github.com/skywind3000/vim-quickui)以了解更多。

## [](#plugin-dedicated-context)<font _mstmutation="1" _msthash="304057" _msttexthash="21031166">插件专用上下文</font>

<font _mstmutation="1" _msthash="290914" _msttexthash="353275156">上下文菜单还可用于增强插件体验，您可以在插件缓冲区设置一些缓冲区本地密钥图：</font>

 <code>let g:context_menu_git = [
 \ ["&Stage (add)\ts", 'exec "normal s"' ],
 \ ["&Unstage (reset)\tu", 'exec "normal u"' ],
 \ ["&Toggle stage/unstage\t-", 'exec "normal -"' ],
 \ ["Unstage &Everything\tU", 'exec "normal U"' ],
 \ ["D&iscard change\tX", 'exec "normal X"' ],
 \ ["--"],
 \ ["Inline &Diff\t=", 'exec "normal ="' ],
 \ ["Diff S&plit\tdd", 'exec "normal dd"' ],
 \ ["Diff &Horizontal\tdh", 'exec "normal dh"' ],
 \ ["Diff &Vertical\tdv", 'exec "normal dv"' ],
 \ ["--"],
 \ ["&Open File\t<CR>", 'exec "normal \<cr>"' ],
 \ ["Open in New Split\to", 'exec "normal o"' ],
 \ ["Open in New Vsplit\tgO", 'exec "normal gO"' ],
 \ ["Open in New Tab\tO", 'exec "normal O"' ],
 \ ["Open in &Preview\tp", 'exec "normal p"' ],
 \ ["--"],
 \ ["&Commit\tcc", 'exec "normal cc"' ],
 \ ]

function! s:setup_fugitive()
    nnoremap <silent><buffer>K :call quickui#tools#clever_context('g', g:context_menu_git, {})<cr>
endfunc

augroup MenuEvents
    au!
    au FileType fugitive call s:setup_fugitive()
augroup END</code> 

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042522" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043081" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291512" _msttexthash="135984121">当您使用逃犯时，您可以按下显示逃犯菜单：</font>```K```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--jolFsSIn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/e3lklalvoaafv31za09k.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--jolFsSIn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/e3lklalvoaafv31za09k.png)

<font _mstmutation="1" _msthash="292110" _msttexthash="192523565">没有必要记住这些很少使用的逃犯关键图， 只是完全足够了。</font>```K```

您还可以为[defx.nvim](https://zshipu.com/t?url=https://github.com/Shougo/defx.nvim)设置上下文菜单：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--UjoMyJV7--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/qj8p0mba7fxzcrwlttav.jpg)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--UjoMyJV7--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/qj8p0mba7fxzcrwlttav.jpg)

这使得 defx 更加人性化。
