---
description: 认识ollydbg
---

# ollydbg动态调试第一篇

### OllyDBG 窗口介绍 <a href="#ollydbg-chuang-kou-jie-shao" id="ollydbg-chuang-kou-jie-shao"></a>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption><p>初始窗口</p></figcaption></figure>

`OllyDBG` 中各个窗口的功能如上图：

* 反汇编窗口：显示被调试程序的反汇编代码，标题栏上的地址、HEX 数据、反汇编、注解可以通过在窗口中右击出现的菜单 界面选项->隐藏标题 或 显示标题 来进行切换是否显示。 用鼠标左键点击注解标签可以切换注解显示的模式
* 寄存器窗口：显示目前选程程的CPU寄存器内容。 同样点击标签 寄存器 （FPU） 可以切换显示寄存器的模式。
* 信息窗口：显示反汇编窗口中选中的第一个指令的参数及一些跳转目的地址、字符串等。
* 资讯窗口：显示内存或档案的内容。 右键菜单可用于切换显示模式。
* 堆栈窗口：显示目前线程的堆叠。

要调整上面各个窗口的大小的话，只需左键按住边框拖曳，等调整好了，重新启动一下就可以生效了。



### 设定UDD、插件路径 <a href="#she-ding-udd-wai-gua-lu-jing" id="she-ding-udd-wai-gua-lu-jing"></a>

启动后我们要把插件及 UDD 的目录配置为绝对路径，点击菜单上的 选项 -> 接口选项，将会出来一个界面选项的对话框，我们点击其中的目录标签：（如果目录标记为空白，先点击其它标签再点回来即可）

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## （第一次使用OD需要启动吾爱破解路径修复工具）

### 调试选项： <a href="#chu-cuo-xuan-xiang" id="chu-cuo-xuan-xiang"></a>

选项 -> 调试选项，新手一般不需变更这里的选项，默认已配置好，可以直接使用。 建议在对已比较熟的情况下再来进行配置。 上面那个异常标签中的选项经常会在脱壳中用到，建议在有一定除错基础后学脱壳时再配置这里。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 右键菜单： <a href="#you-jian-xuan-chan" id="you-jian-xuan-chan"></a>

除了直接启动来调试外，我们还可以把新增到资源管理器右键菜单，这样我们就可以直接在 .exe及.dll 文件上点右键选取「用Ollydbg开启」菜单来进行除错。 要把添加到资源管理器右键菜单，只需点击菜单选项 -> 添加到右键菜单，将会出现一个对话框，先点击「加入Ollydbg 到系统资源管理器菜单」，再点击「完成」按钮即可。 要从右键菜单中移除也很简单，还是这个对话框，点击「从系统资源管理器菜单移除 Ollydbg」，再点击「完成」就行了。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>右键快速打开OD</p></figcaption></figure>

### 插件：

OllyDBG支持插件功能，插件的安装也很简单，只要把下载的插件（一般是个 DLL 文件）复制到安装目录下的 PLUGIN 目录中就可以了，启动时会自动识别。 要注意的是对外挂件的个数有限制，最多不能超过32个，否则会出错。 建议插件不要加入的太多。OllyDBGOllyDBGOllyDBG 1.10

到这里基本配置就完成了，OllyDBG把所有配置都放在安装目录下的ollydbg.ini文件中

### 基本调试方法 <a href="#ji-ben-chu-cuo-fang-fa" id="ji-ben-chu-cuo-fang-fa"></a>

`OllyDBG`有三种模式来装入程序进行调试 ：

* 一种是点击菜单 文件 -> 打开 （快捷键是 F3）来开启一个可执行文件进行调试。
* 另一种是点击菜单 文件 -> 附加 来附加到一个已执行的进程上进行调试。 注意这里要附加的程序必须已执行。
* 第三种就是用右键菜单来加载程序（不知这种算不算）。

一般情况下我们选第一种模式。 比如我们选中一个 来调试，通过菜单 文件 -> 打开 来加载这个程序，中显示的内容将会如下图：

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### 基本快捷键： <a href="#ji-ben-kuai-jie-jian" id="ji-ben-kuai-jie-jian"></a>

* `F2`：设定断点：只要在光标定位的位置（上图中灰色条）按F2键即可，再按一次F2键则会移除断点。 （相当于中的）`SoftICEF9`
* `F8`：单步步过：每按一次这个键执行一条反汇编窗口中的一条指令，遇到等子程序不进入其代码。 （相当于中的）`CALLSoftICEF10`
* `F7`：单步步入：功能同单步步过（）类似，区别是遇到等子程序时会进入其中，进入后首先会停留在子程序的第一条指令上。 （相当于中的）`F8CALLSoftICEF8`
* `F4`：执行到选取位置：作用就是直接执行到光标所在位置处暂停。 （相当于中的）`SoftICEF7`
* `F9`：执行：按下这个键如果没有设定相应断点的话，被调试的程序将直接开始执行。 （相当于中的）`SoftICEF5`
* `CTRL+F9`：执行到返回：此指令在执行到一个（返回指令）指令时暂停，常用于从系统领空返回到我们除错的程序领空。 （相当于中的）`retSoftICEF12`
* `ALT+F9`：执行到用户代码：可用于从系统领空快速返回到我们调试的程序领空。 （相当于中的）`SoftICEF11`

### 额外常用快捷键 <a href="#e-wai-chang-yong-kuai-jie-jian" id="e-wai-chang-yong-kuai-jie-jian"></a>

* 打开一个新可执行程序 （`F3`)
* 重新执行当前调试的程序 （`Ctrl+F2`)
* 当前调试的程序 （`Alt+F2`)
* 运行所选程序进行调试 （`F9`)
* 暂时停止被调试程序的执行 （`F12`)
* 单步进入被调试程序的中 （`CallF7`)
* 步过被调试程序的`Call`(`F8`)
* 和调试程序中 （`CallCtrl+F11`)
* 追踪时略过被调试程序的`Call`(`Ctrl+F12`)
* 执行直到返回 （`Ctrl+F9`)
* 显示日志窗口（ 1）`Alt+L`)
* 显示模块窗口（ 1）`Alt+E`)
* 显示内存窗口 （`Alt+M`)
* 显示 CPU 窗口 （`Alt+C`)
* 显示补缀窗口 （`Ctrl+P`)
* 显示调用堆栈 （`Alt+K`)
* 显示断点窗口（ 1）`Alt+B`)
* 启用调试选项窗口（ 1）`Alt+O`)



注：以上参考了\
[看雪论坛](https://bbs.pediy.com/) 的 [OllyDBG 入门系列（一）-认识OllyDBG](https://bbs.pediy.com/thread-21284.htm)

\
