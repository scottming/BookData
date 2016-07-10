=================
Linux 基础
=================

:Date:   2016-04-03

这一节记录下做数据处理时用到的一些 Linux 和 命令行技巧。大部分命令在 OS
X 系统也适应。

为什么使用 Linux 和命令行
-------------------------

    Have you ever noticed in the movies when the “super hacker,”— you know, the guy who can break into the ultra-secure military computer in under thirty seconds —sits down at the computer, he never touches a mouse? It’s because movie makers realize that we, as human beings, instinctively know the only way to really get anything done on a computer is by typing on a keyboard.

    Most computer users today are only familiar with the graphical user interface (GUI) and have been taught by vendors and pundits that the command line interface (CLI) is a terrifying thing of the past. This is unfortunate, because a good command line interface is a marvelously expressive way of communicating with a computer in much the same way the written word is for human beings. It’s been said that “graphical user interfaces make easy tasks easy, while command line interfaces make difficult tasks possible” and this is still very true today.

    -- The Linux Command Line

Linux 安装和配置
----------------

如果没有任何编程及命令行基础，推荐使用 Ubuntu，有经验后可转
Debian，包多，稳定。进入系统，安装下
`Anaconda <https://anaconda.org/>`__\ [#f1]_，基本的 Python 环境 &
数据工具箱便有了。

再进入终端仿真器，0S X 自带 Terminal，但推荐用 iTerm 2，Debian 是
Konsole，配置下 终极Shell 环境 `Oh My ZSH! <http://ohmyz.sh/>`__

::

    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

如果提示你没有安装相关的依赖包，那么则需先安装相关依赖包，比如 Ubuntu
则需要想安装 Git、和 zsh 等，

::

    sudo apt-get install git zsh

再装个查看数据、转换数据的小工具 csvkit，

::

    sudo apt-get install csvkit

至此，便可开始数据科学之旅了。

基础命令
--------

很多数据问题都可以用命令行解决，而且有些可以解决的非常高效，前提你熟悉一些基础的。
入门级命令，无非这些：

::

    pwd #打印出当前工作目录名
    cd #更改目录
    ls #列出目录内容
    ls #列出目录内容
    file #确定文件类型
    less #浏览文件内容
    cp #复制文件和目录
    mv #移动/重命名文件和目录
    mkdir #创建目录
    rm #删除文件和目录
    ln #创建硬链接和符号链接

    上面的 # 号代表注释，没有任何意义

入门级命令太简单了，就不介绍了，如果从来没碰过命令行，不熟悉使用可以查看帮助，如\ ``ls --help``\ ，另外我推荐些好书。

-  `《笨办法学 Python》 <https://book.douban.com/subject/26264642/>`__
   的附录 `Appendix A: Command Line Crash
   Course <http://learnpythonthehardway.org/book/appendixa.html>`__\ ，Python
   入门靠的就是它，Zed 的这书绝对是神书，附录的 Command Line
   也是写的极好。
-  `The Linux Command Line <https://billie66.github.io/TLCL/book/>`__,
   命令行入门神书，循序渐进，语言幽默，此书激发了我学 Linux 的兴趣。
-  `《Linux
   工具快速教程》 <http://linuxtools-rst.readthedocs.org/zh_CN/latest/index.html>`__\ ，这本书作者写的比较简洁，比较适合有一定编程经验的人。
-  `《鸟哥的 Linux
   私房菜》 <https://book.douban.com/subject/4889838/>`__,
   书虽有点老了，但当做速查手册，翻翻查查，挺好。
-  `《命令行中的数据科学》 <https://book.douban.com/subject/26387975/>`__,
   如何用命令行分析数据的一本书。

重定向和管道符
^^^^^^^^^^^^^^

若你有仔细看过推荐书的任何一本，并做了些许练习，那么你的命令行已经入门了。在介绍命令行处理数据前，我想先谈谈重定向和管道符，若要给
Linux 的符号们举行「频繁使用」比赛，那他们必定是冠军。

平常你在终端里输入\ ``ls -l``\ ，结果应该类似这样：

::

    ➜  Dropbox ls -l
    total 704
    drwxr-xr-x@ 19 Scott  staff   646B Apr  3 10:27 A.HighlyEffectiveSelf
    drwxr-xr-x@  5 Scott  staff   170B Apr  3 09:28 B.CreativePleasure
    drwxr-xr-x@ 10 Scott  staff   340B Apr  3 09:10 C.TheArtOfWork
    drwxr-xr-x@ 11 Scott  staff   374B Mar 10 12:40 D.HistoricalMemory
    drwxr-xr-x@ 12 Scott  staff   408B Apr  3 10:09 E.DataBank
    drwxr-xr-x@ 19 Scott  staff   646B Apr  3 09:14 F.BambooBasket
    drwxr-xr-x@  5 Scott  staff   170B Mar  9 12:34 G.Other
    -rw-r--r--@  1 Scott  staff     0B Apr  3 07:58 Icon?
    -rw-rw-r--@  1 Scott  staff   312B Apr  3 16:18 README.md

文件是文件名排序的，若加个管道符 ``|`` 呢？

::

    ➜  Dropbox ls -l | sort
    -rw-r--r--@  1 Scott  staff     0B Apr  3 07:58 Icon
    -rw-rw-r--@  1 Scott  staff   312B Apr  3 16:18 README.md
    drwxr-xr-x@  5 Scott  staff   170B Apr  3 09:28 B.CreativePleasure
    drwxr-xr-x@  5 Scott  staff   170B Mar  9 12:34 G.Other
    drwxr-xr-x@ 10 Scott  staff   340B Apr  3 09:10 C.TheArtOfWork
    drwxr-xr-x@ 11 Scott  staff   374B Mar 10 12:40 D.HistoricalMemory
    drwxr-xr-x@ 12 Scott  staff   408B Apr  3 10:09 E.DataBank
    drwxr-xr-x@ 19 Scott  staff   646B Apr  3 09:14 F.BambooBasket
    drwxr-xr-x@ 19 Scott  staff   646B Apr  3 10:27 A.HighlyEffectiveSelf
    total 704

这里我加了 ``|`` 和 ``sort``
命令，你会发现，文件的排序已经变了，变成了文件大小的排序。这个命令和简单解释为\ ``ls -l``\ 输出了文件排序结果，而
``sort`` 则接受了这个结果，并把它重新按文件的大小进行了排序，所以
``|`` 就是管道的作用，可以从标准输入读取数据，然后再把数据输送到标准输出。这个特性非常有用，意味着你可以进行非常复杂的操作。

而什么是重定向‘>’呢？你用命令行操作的结果正常是直接显示在屏幕上的，那还有别的方式吗？你试试：

::

    ls -l > ex01.txt

你发现，没有任何动静，但工作目录多了一个 ``ex01.txt`` 的文件，查看下这个文件试试，

::

    ➜  Dropbox cat ex01.txt
    total 704
    drwxr-xr-x@ 19 Scott  staff  646 Apr  3 10:27 A.HighlyEffectiveSelf
    drwxr-xr-x@  5 Scott  staff  170 Apr  3 09:28 B.CreativePleasure
    drwxr-xr-x@ 10 Scott  staff  340 Apr  3 09:10 C.TheArtOfWork
    drwxr-xr-x@ 11 Scott  staff  374 Mar 10 12:40 D.HistoricalMemory
    drwxr-xr-x@ 12 Scott  staff  408 Apr  3 10:09 E.DataBank
    drwxr-xr-x@ 19 Scott  staff  646 Apr  3 09:14 F.BambooBasket
    drwxr-xr-x@  5 Scott  staff  170 Mar  9 12:34 G.Other
    -rw-r--r--@  1 Scott  staff    0 Apr  3 07:58 Icon
    -rw-rw-r--@  1 Scott  staff  312 Apr  3 16:18 README.md
    -rw-rw-r--   1 Scott  staff    0 Apr  3 16:57 ex01.txt

输出结果已经在这个文件里面了，这就是重定向的特性，允许我们来重定义标准输出送到哪里，在‘>’符号后面接个文件名即可。这点是非常实用的，比如你处理完数据后，肯定希望保存到一个文件里面。另外要注意一点，‘>’会格式化原有文件的内容，所以如果你是添加内容，请采用‘>>’。

处理数据常用命令
----------------

行过滤
^^^^^^

若拿到一个很大的数据后，你肯定不想立马查看所有数据，一没必要，而打开慢，而是想做下行过滤，看看一小部分。常用的行过滤命令有\ ``head、tail、seq``\ 。

看前10行数据：

::

    ➜  ~ head user_service_time.txt
    bid service_time    weekday hour    lasttime
    17283201    2016-1-27 8:30:00   3   8   3.0
    17283201    2016-1-29 9:00:00   5   9   3.0
    17283201    2016-2-22 17:00:00  1   17  3.0
    17283201    2016-2-25 16:00:00  4   16  3.0
    17283201    2016-2-29 16:30:00  1   16  3.0
    17283201    2016-3-2 9:00:00    3   9   3.0
    17283201    2014-9-19 9:00:07   5   9
    17283201    2014-11-3 13:00:00  1   13
    17283201    2014-11-22 15:00:00 6   15  3

查看前5行：

::

    head -5 filename

前 n 行：

::

    head -n filename

``tail`` 则跟 ``head`` 刚好相反，查看的是尾行。若需要指定某些行则可用
``sed`` 或 ``awk``\ ，如指定
4-6行，可用\ ``sed -n '4, 6p' filename``\ ，我这里为了好看，用 ``nl``
命令先把行号打印出来。

::

    ➜  ~ nl user_service_time.txt | sed -n '4, 6p'
         4  17283201    2016-2-22 17:00:00  1   17  3.0
         5  17283201    2016-2-25 16:00:00  4   16  3.0
         6  17283201    2016-2-29 16:30:00  1   16  3.0
    # 查看奇数行
    ➜  ~ nl user_service_time.txt | head |  awk 'NR%2'
         1  bid service_time    weekday hour    lasttime
         3  17283201    2016-1-29 9:00:00   5   9   3.0
         5  17283201    2016-2-25 16:00:00  4   16  3.0
         7  17283201    2016-3-2 9:00:00    3   9   3.0
         9  17283201    2014-11-3 13:00:00  1   13
    # 偶数行
    ➜  ~ nl user_service_time.txt | head |  awk '(NR+1)%2'
         2  17283201    2016-1-27 8:30:00   3   8   3.0
         4  17283201    2016-2-22 17:00:00  1   17  3.0
         6  17283201    2016-2-29 16:30:00  1   16  3.0
         8  17283201    2014-9-19 9:00:07   5   9
        10  17283201    2014-11-22 15:00:00 6   15  3

列提取
^^^^^^

行提取很简单，那么列提取应该如何做呢？

::

    # 把所有缩进符号改为逗号(英文）， 再重定向成 csv 文件, .txt 文件可用 cat，excel 文件则需 in2csv
    cat user_service_time.txt | tr '/t' ',' > user_service_time.csv

    # 看看前 3 行，有哪些列
    ➜  ~ head -3 user_service_time.csv | csvlook
    |-----------+--------------------+---------+------+-----------|
    |  bid      | service_time       | weekday | hour | lasttime  |
    |-----------+--------------------+---------+------+-----------|
    |  17283201 |  2016-1-27 8:30:00 |  3      |  8   |  3.0      |
    |  17283201 |  2016-1-29 9:00:00 |  5      |  9   |  3.0      |
    |-----------+--------------------+---------+------+-----------|
    # 得知总共有 5 列提取后 3 列 的前 10 行看看
    ➜  ~ < user_service_time.csv csvcut -c 3-5 | head | csvlook
    |----------+------+-----------|
    |  weekday | hour | lasttime  |
    |----------+------+-----------|
    |   3      |  8   |  3.0      |
    |   5      |  9   |  3.0      |
    |   1      |  17  |  3.0      |
    |   4      |  16  |  3.0      |
    |   1      |  16  |  3.0      |
    |   3      |  9   |  3.0      |
    |   5      |  9   |           |
    |   1      |  13  |           |
    |   6      |  15  |  3        |
    |----------+------+-----------|
    # 也可以用 -C 来忽略某些行，如忽略 3-5 列的前5行。
    ➜  ~ < user_service_time.csv csvcut -C 3-5 | head -5 | csvlook
    |-----------+----------------------|
    |  bid      | service_time         |
    |-----------+----------------------|
    |  17283201 |  2016-1-27 8:30:00   |
    |  17283201 |  2016-1-29 9:00:00   |
    |  17283201 |  2016-2-22 17:00:00  |
    |  17283201 |  2016-2-25 16:00:00  |
    |-----------+----------------------|

grep 查找
^^^^^^^^^

::

    # 基本用法是 grep data filename
    ➜  ~ head user_service_time.txt | grep 29
    17283201    2016-1-29 9:00:00   5   9   3.0
    17283201    2016-2-29 16:30:00  1   16  3.0

wc 基本统计
^^^^^^^^^^^

-  统计行数 wc -l file
-  统计单词数 wc -w file
-  统计字符数 wc -c file

::

    ➜  ~ wc -l user_service_time.txt
        1244 user_service_time.txt
    ➜  ~ < user_service_time.txt | grep 2016-2 | wc -l
          55

sort 排序
^^^^^^^^^

-  -n 按数字进行排序
-  -d 按字典序进行排序
-  -r 逆序排序
-  -k N 指定按第N列排序

::

    # 以第 1 列数字反向排序
    ➜  ~ < user_service_time.csv | sort -nrk 1 | head -4 | csvlook
    |-----------------+-------------------+---+---+----|
    |  29101041557001 | 2016-3-6 8:30:00  | 7 | 8 | 4  |
    |-----------------+-------------------+---+---+----|
    |  29101041557001 | 2016-3-13 8:30:00 | 7 | 8 | 4  |
    |  29101041557001 | 2016-2-28 8:30:00 | 7 | 8 | 4  |
    |  29101041557001 | 2016-2-21 8:30:00 | 7 | 8 | 4  |
    |-----------------+-------------------+---+---+----|

其他
----

``iconv`` ``cut`` ``past`` ``uniq``
等工具也是极好的，只不过用的略少，具体的数据分析则用 Pandas 更方便些。其他的，想到再添加。

.. rubric:: Footnotes

.. [#f1] 一个打包好 Python 科学计算常用包的平台工具，安装它，也就拥有了Python、NumPy、SciPy、Matplotlib、IPython、Jupyter 等。
