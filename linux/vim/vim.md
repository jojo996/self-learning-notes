# VIM

![wAUpUM-1](D:\Desktop\typora\imgs\wAUpUM-1.png)

[![vi-vim-cheat-sheet-sch](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch1.gif)](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch1.gif)

## 文件操作

```shell
vim file1 file2
:ls //列出所有vim打开的文件
:bn //显示第n个文件

//一次性打开多个文件
vim -On file1 file2 ... filen //左右分屏
vim -on file1 file2 ... filen //上下分屏

//分屏 (ctrl+w) + (?)
s 		//上下分割当前文件
:sp file //上下分割当前文件和新文件
v 		//左右分割当前文件
:vsp file //左右。。。。

h //光标定位左边
l //右边
j //光标移动到下面的分屏
k //上面

H //分屏左移
L //右移
J //下移
K //上移

c // 关闭当前分屏
q // 关闭当前分屏+如果是最后一个就退出vim

//退出
:w		//保存
:w!		//强制保存
:w file	//保存当前修改到file中
:q		//退出不保存
:qa		//退出所有文件不保存
:q!	
:qa!	

:wq		//保存退出
:x		//还是保存退出
ZZ		//同上

:e file	//打开另一个文件
:e!		//放弃这次所有修改
:saves file	//另存为file
:bn :bp		//文件上一个/下一个切换
```

## 普通模式

### 编辑文本

```shell
// 进入插入模式
i //光标左
I //行首
a //光标右
A //行尾
o //下行行首
O //上行行首
s //删除字符插入
S //删除行插入
cw //删除到单词结束插入
```

**在当前行上移动光标**

`0` 移动到行头
`$`  移动到行尾
`^`   移动到本行的第一个不是 blank 字符
`g_`  移动到本行最后一个不是 blank 字符的位置

`w` 光标移动到下一个单词的开头
`e`  光标移动到下一个单词的结尾

`fa`  移动到本行下一个为 a 的字符处，fb 移动到下一个为 b 的字符处
`nfa` 移动到本行光标处开始的第 n 个 字符为 a 的地方（n 是 1，2，3，4 ... 数字）
`Fa` 同 `fa` 一样，光标移动方向同 `fa` 相反
`nFa` 同 `nfa` 类似，光标移动方向同 `nfa`相反

`ta` 移动光标至 a 字符的前一个字符
`nta` 移动到第二个 a 字符的前一个字符处
`Ta` 同 `ta` 移动光标方向相反
`nTa` 同 `nta` 移动光标方向相反

重复搜索
`;` 和`,` 当使用 f, F, t ,T, 关键字指定字符跳转的时候，使用 `;`可以快速跳转到写一个指定的字符，`, ` 是跳到前一个指定的字符


**跨行移动光标**

`nG ` 光标定位到第 n 行的行首
`gg ` 光标定位到第一行的行首
`G `  光标定位到最后一行的行首gt


`H ` 光标定位到当前屏幕的第一行行首
`M`   光标移动到当前屏幕的中间
`L` 光标移动到当前屏幕的尾部

`zt` 把当前行移动到当前屏幕的最上方，也就是第一行
`zz` 把当前行移动到当前屏幕的中间
`zb` 把当前行移动到当前屏幕的尾部

`%`   匹配括号移动，包括 ( , { , [  移动到这个括号的另一半那里，需要把光标先移动到括号上
`*` 和 `#` 匹配光标当前所在的单词，移动光标到下一个（或者上一个）匹配的单词（ `*` 是下一个，`#` 是上一个）

**翻页操作**

`ctrl+f` 查看下一页内容

`ctrl+b` 查看上一页内容

**VIM 的复制，黏贴 ，删除**

三个重要的快捷键 `d` , `y` , `p`

`d` 是删除的意思，通常搭配一个字符 ( 删除范围 ) 实现删除功能，常用的如下：

`dd` 删除一整行

`dw` 删除一个单词

`dnw` 删除 n 个单词

`dfa` 删除光标处到下一个 a 的字符处（ fa 定位光标到 a 处 ）

`dnfa` 删除光标处到第 n 个 a 的字符处

`ndd` 删除光标处开始的 n 行

`d$` 删除光标到本行的结尾

`dH` 删除屏幕显示的第一行文本到光标所在的行

`dG` 删除光标所在行到文本的结束



`y` 是复制的意思，通常搭配一个字符（复制范围）实现复制的功能，常用的如下：

`yw` 复制一个单词，还有 `ynw`

`yfa` 复制光标到下一个 a 的字符处,还有`ynfa`

`yy` 复制一行，还有 `nyy`

`y$` 复制光标到本行的结尾

`yH` 复制屏幕显示的第一行文本到光标所在的行

`yG` 复制光标所在行到文本的结束



`p` ，`P`是黏贴的意思，当执行完复制或者黏贴的命令以后，VIM 会把文本寄存起来。

p 在光标后开始黏贴

P 光标前开始粘贴



**撤销操作和恢复**

`u` 撤销刚才的操作

`ctrl + r` 恢复撤销操作 // 但是我自定义成ctrl + y了



**删除字符操作和替换**

`x` 删除光标当前所在的字符

`r` 替换掉光标当前所在的字符

`R` 替换掉从光标开始以后的所有字符，除非 `<ESC >` 退出，或者 `jj` （代替 <ESC> 上文有提到）退出。



**大小写转换**

~ 将光标下的字母改变大小写	
3~ 将光标位置开始的3个字母改变其大小写
g~~ 改变当前行字母的大小写
gUU 将当前行的字母改成大写
guu 将当前行的字母全改成小写

3gUU 将从光标开始到下面3行字母改成大写
gUw 将光标下的单词改成大写。
guw 将光标下的单词改成小写



**VIM 的重复命令**

. 该命令是重复上一个操作的命令
n<command>重复某个命令 n 次，
如 10p复制 10 次，10dd 删除十次。



## 可视化模式

v,V,Ctrl+v 

v字符可视化，按下键盘上的v以后，屏幕底部应该会有一个 VISUAl 的提示，操作 h,j,k,l就选中文本，继续按 v 退出可视化模式。

V 行可视化，按下键盘上的 V 以后，屏幕底部应该有一个 VISUAL LINE 的提示，操作 j,k 可以向上或者向下以行为单位选中文本，继续按下 V 退出可视化模式。

Ctrl+v 块状可视化，按下键盘上的 Ctrl+v 以后，屏幕底部应该会有一个提示 VISUALBLOCK ，可以通过 h,j,k,l 块状的操作选择区域，这是很多编辑器都不可以做到的，继续按下 Ctrl+v 会退出可视化模式。


**可视化模式下操作文本**

可视化模式下选择操作区域以后，
按下 d会删除选择的区域，
按下 y 会复制选择的区域，按下 p 会黏贴选择的区域。


**可视化模式下 v 的特殊操作**

当操作的文本光标在 “”，‘’ ，（），{} ，[（双引号，单引号，小括号，大括号，中括号）
当中的时候,可以通过 va"选中 ”“ 内的所有内容包括双引号 ，vi" 选中 "" 内的所有内容，不包括 ""。va,vi 会快速选择区域，va 后面会紧跟一个区域结束标志，a 会选中结束符标志，i 就不会。例子如下：

"hello world [VI**M** is so strong],{we all can master vim skill}"

假设当前光标定位在上面的文本 M 处：
va] 操作将会选中以下文本（加粗部分）：
“hello world***[VIM is so strong]\***,{we all can master vim skill}“
vi] 操作将会选中如下的区域，没有包含 []：
“hello world [***VIM is so strong\***],{we all can master vim skill}“


**块区域下的特殊操作**

Ctrl+v 选中块区域以后，按下大写的 I 或者 A 可以在区域的前面或者后面输入内容，按下 jj 或者 <ESC>,可以看到选中的区域前面或者后面会有输入的内容。


## 命令模式

```sh
// 行命令
:set nu   //显示行号
:set nonu //取消显示

:n  	//定位到n行

# 查找
# \<表示字符串开头，\>表示结尾，可以用作全词匹配
/{目标字符串}  	//匹配目标字符串高亮
:set ic 		//不区分大小写
:set noic		//区分


# 替换
:{作用范围}s/{源字符}/{替换字符}/{替换标志}

// 作用范围
s 当前行
%s 全文
n1,n2s    //这里的 n1 和 n2 值得是行号，将会替换掉 n1 到 n2 的所有 zempty 为 handsome.
选区，在可视模式下选择区域后输入 : ，VIM 会自动补全为 :'<,'> ,然后需要手动补充一个s
:'<,'>s/zempty/handsome/g

// 替换标志
空	从光标往后的第一次出现
i 大小写不敏感 I 敏感 //ignorange
g 所有出现
c 需要确认
例子：gci 需要确认的大小写敏感的所有出现
```



### VIM 执行 Linux 命令



```
:!command
```

`:` 后面紧跟着 `!` ，`!` 后面紧跟着 linux 命令（ command 指操作 Linux 系统的一系列命令，如创建文件，新建文件夹，查询文件的属性的等），例子如下，

```
 :!date
```

执行 date 命令显示时间，执行完命令以后按下键盘上的 Enter 就会返回到文件。



VIM 执行命令，并且添加结果至操作文本光标处

```
:r !command
```

: 后面紧跟着 r , r 后面是空格，紧接着是  !command( command 解释同上)，例子如下，

```
:r !date 
```

执行 date 命令显示时间，并且添加命令结果到文本中。



### 定义快捷键

下面举例说明：

```
:map ^M I#<ESC>
```

上面的例子也就是通过快捷键 `Ctrl + m` 在文件光标处所在行的行首插入 # （ # 代表注释）。

`:` 后面的 map 是关键字 ，后面是 key 和 value 。

key 对应的是 ^M ， 这个 key 需要强调一下 ^M 是 Ctrl + v + m 打出来的（按下这三个键，VIM 会显示成 ^M ）,^M 代表快捷键是`Ctrl + m` , Ctrl + v + n 就是  ^N ,代表快捷键是 Ctrl + n 。Ctrl + v + x 就是 ^X (这里的 x 是代表 26 个字母中的任意一个) 代表快捷键 `Ctrl + x`。

value 对应的是 `I#<ESC>`,表示按下快捷键以后执行的相应操作，`I` 是切换光标至行首并切换到编辑模式，`#`是行首输入的内容（ # 是VIM 文件中的注释符号 ），`<ESC>` 是退出编辑模式。 



举例如下：

`:map ^D Ahelloworld<ESC>`表示在文件的光标所在行的行尾，添加 helloworld 字符串，按住组合键 ctrl + d 就会执行操作。



### 使用 ab

```
:ab cnm caonima
```

`:` 后面的 ab 是关键字 ,该命令执行后，然后切换到编辑模式下

输入 cnm 会把输入的 email 自动替换成 caonima。

这个命令主要是==处理频繁输入==同样的长串字符串。



## **VIM 的代码提示功能**

在编辑模式下 ，快捷键 Ctrl+n 或者 Ctrl+p 会有代码提示功能，我们可以实现快速录入的效果。



## **VIM 的宏录制**

假设需要操作的文本如下,需要将如下文本的每一行的行首插入入一个 tab 键。

hello 
hello world
hello world , vim 

**宏录制的录制操作**

先将光标移动到第一行，在普通模式下按下 q 键（**宏录制是 q 键启动的**),在按一个 a （字母随意）,表示该宏注册为 a  ，按下 I 在行首插入一个 tab 键，按下jj或者 <ESC>退出编辑模式,按下 j 将光标移动到下一行行首，最后按下 q 键完成录制操作（**宏录制是 q 键结束的**）。
总结上面例子的操作流程：
q → a → I → tab → jj → j → q
上面的例子成功地把在行首插入 tab 的功能录制了下来，那么如何应用到其他行呢？

**宏录制的使用**

上述的例子，在正常模式下，按 @a执行宏录制的一系列动作，将会在第二行执行插入 tab 。
@@ 是对上一次宏使用的重复操作。n@a 就会执行 n 次一系列的动作。使用宏录制可以一次执行一系列的操作，可以针对一些重复度较高的操作进行宏录制。

















