
title: Django实战系列：如何创建新的 Django 项目：分步指南
author: 知识铺
date: 2020-10-07 18:17:24
tags: 
---
 _这适用于 Windows 用户。我使用```cmd 和```VS 代码终端来编写我的命令。请确保您在计算机上```安装了 Python``` ```、pip（Python```的包管理器 - 就像```npm```是 Javascript）和```Visual Studio 代码```，并在 VS 代码中启用了 Python 扩展码。我假设您熟悉 Python 和命令行/如何编写基本命令。_

**我们要实现什么：**

1.  安装虚拟环境（我将解释一下该环境是什么）
2.  <font _mstmutation="1" _msthash="440934" _msttexthash="137796737">激活/停用虚拟环境（之后使用第一个和 VS 代码）</font>```cmd```
3.  安装 Django
4.  创建新的 Django 项目

**安装虚拟环境并处理它**

<font _mstmutation="1" _msthash="276809" _msttexthash="235155297">**第一步：**导航到 Django 项目及其所有依赖项将驻留并安装 的文件夹。</font>```virtual environment```

> <font _mstmutation="1" _msthash="734539" _msttexthash="956660653">虚拟环境（也称为 Python 环境）是 Python 环境，因此安装到其中的 Python 解释器、库和脚本与其他虚拟环境中的脚本隔离。Python 虚拟环境的核心目的是</font>```venv``````to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.```

<font _mstmutation="1" _msthash="277381" _msttexthash="1701955580">我的桌面上有一个名为 Django 项目文件夹， 所以我要打开一个内部。所以，你这样做：打开你的文件夹，点击Windows资源管理器的位置栏，并键入。命令行窗口应出现，这样之后发生类型，如：</font>```cmd``````cmd``````pip install virtualenv```

 <code>C:\Users\Silvia\Desktop\DjangoProjects>pip install virtualenv</code> 

<font _mstmutation="1" _msthash="277953" _msttexthash="2198077518">这将安装，但它不会激活它（我们将在一点点做到这一点）。在控制台中，您应该看到一条消息，显示 。我们可以创建和激活尽可能多的，因为我们希望从现在开始，一个条件，他们都留在这个文件夹（在我的情况下，在Django项目）。</font>```virtual environment``````Successfully installed virtualenv + the version number``````venvs```

<font _mstmutation="1" _msthash="290017" _msttexthash="630760364">**第二步：**为新的 Django 项目创建一个文件夹。在我的 Django 项目文件夹中，我将创建一个名为 的新目录，以便键入 ：</font>```my_website``````cmd```

 <code>C:\Users\Silvia\Desktop\DjangoProjects>mkdir my_website</code> 

<font _mstmutation="1" _msthash="290615" _msttexthash="84215768">**第三步：**导航到新创建的文件夹：</font>

 <code>C:\Users\Silvia\Desktop\DjangoProjects>cd my_website</code> 

<font _mstmutation="1" _msthash="291213" _msttexthash="1744300350">**第四步：**该文件夹现在为空，因此让我们在它内部创建一个文件夹（我们现在创建的第 venv 将仅在此特定目录中工作）。我会叫我的 venv （名字是随机的， 你可以叫它任何你想要的） 。创建 venv 的命令是 = 环境的名称。</font>```virtual environment``````env1``````py -3 -m venv```

 <code>C:\Users\Silvia\Desktop\DjangoProjects\my_website>py -3 -m venv env1</code> 

<font _mstmutation="1" _msthash="291811" _msttexthash="2395810599">**第五步：**虚拟环境已经创建，但我们并没有真正得到任何响应在控制台告诉我们，所以检查它，打开你的项目文件夹，并检查其内容（或键入和您将在你的目录内的内容）。您应该会看到一个文件夹，该文件夹的名称为 venv。让我们在它里面导航：</font>```dir``````cmd```

 <code>C:\Users\Silvia\Desktop\DjangoProjects\my_website>cd env1</code> 

<font _mstmutation="1" _msthash="292409" _msttexthash="154805352">该文件夹内应有两个目录和两个文件，并且应类似：</font>```env1```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--WHR8JZOn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6dxt0noo05tlig6xb2ll.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--WHR8JZOn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6dxt0noo05tlig6xb2ll.PNG)

<font _mstmutation="1" _msthash="290303" _msttexthash="2459092376">要激活虚拟环境，我们必须使用文件夹中的文件并键入命令。我以不同的方式看到这样做，但很多时候，我迷失了所有需要键入的完整路径的斜杠，所以我这样做的方式是通过在文件夹中导航，并直接在那里运行命令。因此，我们必须做类似：</font>```activate.bat``````Scripts``````activate.bat``````Scripts``````activate.bat```

 <code>C:\Users\Silvia\Desktop\DjangoProjects\my_website\env1>cd Scripts
C:\Users\Silvia\Desktop\DjangoProjects\my_website\env1\Scripts>activate.bat</code> 

<font _mstmutation="1" _msthash="290901" _msttexthash="85603245">现在，我们将看到类似的东西在 ：</font>```cmd```

 <code>(env1) C:\Users\Silvia\Desktop\DjangoProjects\my_website\env100\Scripts></code> 

<font _mstmutation="1" _msthash="291499" _msttexthash="543635989">因此，您知道 已激活的 que 是在其路径前的括号中、控制台中查看其名称。到 venv 的方法是在文件夹内键入命令行：</font>```venv``````deactivate``````deactivate``````Scripts```

 <code>(env1) C:\Users\Silvia\Desktop\DjangoProjects\my_website\env1\Scripts>deactivate</code> 

现在，我们已经安装并创建了 venv 并了解如何激活和停用它，我们将转到 VS 代码来安装 Django 并创建一个项目。

**在 VS 代码中工作、安装 DJANGO 和创建项目**

**第六步**使用 VS 代码打开项目文件夹。此时，您内部唯一拥有的内容是虚拟环境目录。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--9s_a-349--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/m8nta5rlgs65gedg8dm3.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--9s_a-349--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/m8nta5rlgs65gedg8dm3.PNG)

<font _mstmutation="1" _msthash="290589" _msttexthash="369186376">让我们激活 。为此，请转到 。您将看到选项列表。您应该选择一个在其中提及虚拟环境的人。</font>```venv``````View -> Command Pallete -> Python: Select Interpreter```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--peT4O4Bp--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/kpd76ou6yhbqvcj4spow.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--peT4O4Bp--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/kpd76ou6yhbqvcj4spow.PNG)

<font _mstmutation="1" _msthash="291187" _msttexthash="664052922">现在，如果您打开一个新的终端（转到终端 -> 新终端），您将在圆形括号中看到环境的名称，因此这意味着环境已激活。</font>

 <code>(env1) PS C:\Users\Silvia\Desktop\Django\my_website></code> 

<font _mstmutation="1" _msthash="291785" _msttexthash="106018913">**第七**
步让我们现在安装 Django 。在终端中键入 。</font>```pip install django```

 <code>(env1) PS C:\Users\Silvia\Desktop\Django\my_website> pip install django</code> 

<font _mstmutation="1" _msthash="292383" _msttexthash="858408525">安装需要一段时间才能完成，完成后，您可以在终端中键入，看看安装是否成功，以及您使用的 Django 版本。在我写这篇文章的时候，我使用。</font>```python -m django --version``````Django 3.1.2```

<font _mstmutation="1" _msthash="292682" _msttexthash="484421626">**最后，**
让我们创建一个 Django 项目。为此，我们必须使用项目命令的 + 所需的名称。我会打电话给我的。</font>```django-admin startproject``````my_blog```

 <code>(env1) PS C:\Users\Silvia\Desktop\Django\my_website> django-admin startproject my_blog</code> 

项目几乎可以立即创建，如果您现在在 VS 代码中的"资源管理器"窗口中查看，您将看到一个包含您为项目选择的名称的新文件夹。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--LmPxcWVR--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/t5mk71a8olmb5ghpvkvv.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--LmPxcWVR--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/t5mk71a8olmb5ghpvkvv.PNG)

<font _mstmutation="1" _msthash="291174" _msttexthash="177310731">打开该文件夹后，您会看到另一个同名的文件夹和名为 的文件。</font>```manage.py```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--AAPS8-e3--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fmzgcaa802tbnxc0spsa.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--AAPS8-e3--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fmzgcaa802tbnxc0spsa.PNG)

<font _mstmutation="1" _msthash="291772" _msttexthash="836206527">我不太了解详情，但所有您需要了解的是，此文件可以在新 Django 项目的每个根目录中找到，它有助于运行命令。所以，很多时候你会写类似 。</font>```python manage.py + some command```

<font _mstmutation="1" _msthash="292071" _msttexthash="1176472245">Django 的好东西是它配备了专用服务器，因此我们可以立即开始编写和测试代码（我们将在本地计算机上运行模拟服务器）。我们启动服务器的方式是使用以下命令：</font>```python manage.py runserver```

 <code>(env1) PS C:\Users\Silvia\Desktop\Django\my_website\my_blog> py manage.py runserver</code> 

<font _mstmutation="1" _msthash="292669" _msttexthash="596702522">**重要提示**：您必须在 Django 项目的 ROOT 中运行此内容，否则您会收到错误（请注意，我导航到文件夹中）。</font>```manage.py``````my_blog```

<font _mstmutation="1" _msthash="292968" _msttexthash="645113326">完成操作后，您将在终端中收到一条消息，说 。复制并粘贴该地址到您的浏览器，如果一切顺利，你应该看到类似：</font>```Starting development server at http:// + some IP address```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--owy-sB9_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/7gvqpe7zbtfr3t6mp3d9.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--owy-sB9_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/7gvqpe7zbtfr3t6mp3d9.PNG)

恭喜你，您已经成功地创建了一个新的 Django 项目😊。


