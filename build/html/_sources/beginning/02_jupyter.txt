Jupyter 的安装和使用
====================

:Date:   2016-04-04

IPython 和 Jupyter
------------------

IPython 是一个 Python REPl shell，环境远比 Python 自带的强大，而 Jupyter
Notebook 则是一个基于 IPython REPl 的 Web
应用，运行结果可保存为后缀.ipynb，交互性强，所见即所得，数据分析，写分析报告等的不二利器。

官方解释：

    The Jupyter Notebook is a web application that allows you to create
    and share documents that contain live code, equations,
    visualizations and explanatory text. Uses include: data cleaning and
    transformation, numerical simulation, statistical modeling, machine
    learning and much more.

安装
----

如果有看过我上一篇文章 `《用 Linux
处理数据》 <http://scottming.com/2016/04/03/use_linux/#linux--1>`__
，并安装了
`Anaconda <https://www.continuum.io/downloads>`__\ ，那么你已经有
Jupyter 了，打开终端，输入 ``jupyter notebook`` 即可。

远程使用
^^^^^^^^

如果有远程使用的需求，则需把远程服务器配置下。

::

    # 服务器下载 ssh 服务，如 Debian
    sudo apt-get install openssh-server
    # 不知道 ssh 是否打开，可以把他重启下
    sudo service sshd restart

然后可以在局域网用其他电脑访问下，Mac 可直接在终端输入
``ssh username@ip``, 这里的 ip 指的局域网下的这台服务器的
ip，建议在路由器设置成静态
ip，若在外网使用，则需在路由器里面设置好端口转发。

然后参考官方教程 `Running a notebook
server <http://jupyter-notebook.readthedocs.org/en/latest/public_server.html>`__
配置。

.. Attention:: jupyter\_notebook\_config.py 这个文件里面 certfile 和 keyfile 的地址应为绝对地址.

一大串输入很麻烦，也易出错，建议打开 .zshrc，并在底部添加一行：

::

    alias jn='jupyter notebook --certfile=/home/scott/.jupyter/mycert.pem --keyfile /home/scott/.jupyter/mykey.key'

这样到其他电脑键入：

::

    jn

若能看到类似下方的输出，证明配置成功了。

::

    [I 09:56:29.937 NotebookApp] The Jupyter Notebook is running at: https://[all ip addresses on your system]:8889/

我的端口配置的是 ``8889``\ ，
你也可以设置成其他的，再到路由器里配置下端口转发，大功告成。如果有用
R，也可用类似的方法配置下 `RStudio
Server <https://www.rstudio.com/products/rstudio/download-server/>`__\ ，超简单。

快捷操作
--------

Jupyter Notebook 的快捷键是一大亮点，如果有看过我这篇文章 `《让 CapsLock
键更实用》 <http://scottming.com/2016/01/01/remap_keyboard/>`__\ [#f1]_ ，并对 Mac 或 Win 做了配置，那么你熟悉几个
Jupyter 的快捷，用 Jupyter 写报告之类基本上不需要鼠标了。

单元类型 (cell type)
^^^^^^^^^^^^^^^^^^^^

``Jupyter Notebook``\ 文档由一系列的单元 (cell)
组成，主要用的两类单元是：

-  ``markdown cell``\ ，命令模式下，按 ``m`` 可将单元切换为
   ``markdown cell`` 。
-  ``code cell``\ ，命令模式下，按 ``y`` 可将单元切换为 ``code cell`` 。

常用快捷
^^^^^^^^

-  查看快捷键帮助: ``h``
-  保存: ``s``
-  cell 间移动: ``j``, ``k``
-  添加 cell: ``a``, ``b``
-  删除 cell: ``dd``
-  cell 编辑: ``x``, ``c``, ``v``, ``z``
-  中断 kernel: ``ii``
-  重启 kernel: ``00``
-  注释 code: ``Ctrl + /``

拆分单元 (split cell)
^^^^^^^^^^^^^^^^^^^^^

编辑模式下按 ``control + shift + -`` 可拆分 c ell

查看对象信息
------------

.. code:: python

    import numpy as np

按 ``tab`` 键查看提示信息

.. code:: python

    np.<tab>

查找 ``numpy`` 模块下，名称含有 ``cos`` 的对象

.. code:: python

    np.*cos*?

提供 numpy 模块的帮助信息

.. code:: python

    np?

提供 numpy 模块更详细的帮助信息

.. code:: python

    np??

查看 docstring

.. code:: python

    %pdoc np

魔术命令
--------

最常用的是这个 ``%matplotlib inline``\ ，有点类似
``ipython --pylab``\ ，画图用的；测试程序运行时间则只需把 ``%time``
放在前面。

更多魔术命令可在 Jupyter Notebook 里键入：

.. code:: python

    %lsmagic

转换
----

::

    # ipynb 文件转为 html
    jupyter nbconvert --to html filename.ipynb

更多转换内容，请键入：

::

    jupyter notebook --help

转换 rst、py、md 等格式都是非常方便的，但转
pdf，对中文的支持不好。必须先装 LaTex，LaTex 则需先把字体等调好。

.. rubric:: Footnotes

.. [#f1] 让键盘更高效的一篇文，昨天顺手把karabiner 配置的 gist 更新了。
