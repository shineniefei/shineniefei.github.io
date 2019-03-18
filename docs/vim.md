---
title: vim
---

# VIM使用

## 写在前面

内容来自网络总结

## 状态模式

| 按键 | 作用 |
| :-: | :-- |
i | 进入 插入 模式
ni | 进入 重复插入 模式
ESC | 返回 命令 模式
v | 进入 可视 模式
V | 进入 行可视 模式
CTRL+v | 进入 块可视 作模式
Ixxx | 在被选中的块的前面插入xxx
0Ixxx | 在被选中的块的每一行的行首插入xxx
Axxx | 在被选中的块的后面追加xxx

## 光标控制

| 按键 | 作用 |
| :-: | :-- |
k | 向上移一行
j | 向下移一行
h | 向左移一列
l | 向右移一列
nk | 向上移动n行
nh | 向左移动n列
gg | 移到到第一行
G | 移到文件的最后一行
nG或`:`n | 移到文件的第n行
L | 移到屏幕的最后一行
M | 移到屏幕的中间一行
H | 移到屏幕的第一行
( | 移到句子的开头
) | 移到句子的结尾
{ | 移到段落的开头
} | 移到下一个段落开头
% | 移动到与制匹配的括号上去（），{}，[]，<>等
0 | 移到当前行的开头
n`|` | 移到当前行的第n列
$ | 移到当前行的最后(块模式下，$将块选择中的每一行都扩展至行尾)
n$ | 移动到第n行的行尾
^ | 移到当前行的第一个非空字符
e | 向后移一个单词到结尾
ne | 向后移n个单词到结尾
E | 向后移一个单词到结尾，忽略标点符号
b | 向前移一个单词到开头
nb | 向前移n个单词到开头
B | 向前移一个单词到开头，忽略标点符号
w | 向后移一个单词到开头
W | 向后移一个单词到开头，忽略标点符号
+或Enter | 移到下一行的第一个字符
`-` | 移到前一行的第一个非空字符
[[ | 光标跳转到代码块开头即{处,要求{独占一行
gD | 光标跳转到局部变量定义处
'' | 光标跳转到上次停靠处
ggVG | 全选文本
gg=G | 排版文本

## 屏幕调整

| 按键 | 作用 |
| :-: | :-- |
H | 将光标移动到屏幕的顶行
nH | 将光标移动到屏幕顶行下的第n行
M | 将光标移动到屏幕的中间
L | 将光标移动到屏幕的底行
nL | 将光标移动到屏幕底行上的第n行
CTRL+e | 将屏幕上滚一行
CTRL+y | 将屏幕下滚一行
CTRL+u | 将屏幕上滚半页
CTRL+d | 将屏幕下滚半页
CTRL+b | 将屏幕上滚一页
CTRL+f | 将屏幕下滚一页
CTRL+l | 重绘屏幕
z+RETURN | 将光标所在的那一行移至屏幕顶部
z-RETURN | 将当前行置为屏幕的顶行
nz-RETURN | 将当前行下的第n行置为屏幕的顶行
z. | 将当前行置为屏幕的中央
nz. | 将当前行上的第n行置为屏幕的中央
z- | 将当前行置为屏幕的底行
nz- | 将当前行上的第n行置为屏幕的底行

## 插入文本

| 按键 | 作用 |
| :-: | :-- |
a | 在光标后插入文本
i | 在光标前插入文本
A | 在当前行尾插入文本
I | 在当前行首插入文本
o | 在当前行的下边插入新行
O | 在当前行的上边插入新行

## 删除文本

| 按键 | 作用 |
| :-: | :-- |
x或dl | 删除光标处的字符
nx | 从当前光标处往后删除n个字符
X或dh | 删除光标前的字符
nX | 从当前光标处往前删除n个字符
d | 剪切删除文字
D | 从光标定位的行末删除文本
dw | 删至下一个字的开头
ndw | 从当前光标处往后删除n个字
dG | 删除行，直到文件结束
dd | 删除整行
dj | 删除上一行
dk | 删除下一行
ndd | 从当前行开始往后删除n行
db | 删除光标前面的字
ndb | 从当前行开始往前删除n字
de | 删除一个单词
d$ | 从光标处删除到行尾
d1G | 删除光标所在行到第一行的所有数据
dgg | 删除当前行到文件首部的所有行(包括当前行)
jdG | 删除当前行之后所有行（包括当前行）
`:`n,md | n到m行之间的行（可用%或0,$表示全文）
CTRL+w | 插入模式下，删除前面的字

## 修改文本

每个命令前面的数字表示该命令重复的次数

| 按键 | 作用 |
| :-: | :-- |
rCHAR | 用CHAR替换当前字符
R | 从当前字符开始替换直到按下Esc键
s | 删除当前字符并插入
S或cc | 取代光标所在整行
cw | 删除当前单词并插入
C | 删除光标处到行尾字符并插入
cG | 删除光标处到末尾并插入
c0或c^ | 删除光标处到到行首并插入,不包括光标处字符
`:`1, 10 m 20 | 将第1-10行移动到第20行之后
`~` | 交换大小写

## 复制文本

| 按键 | 作用 |
| :-: | :-- |
yy或Y | 将当前行的内容放入临时缓冲区（yank命令）
nyy | 将n行的内容放入临时缓冲区
yw | 把光标当前所在的单词移到缓冲区
y$ | 把当前行及其以前的所有文本移到缓冲区
p | 将临时缓冲区中的文本放入光标行下
P | 将临时缓冲区中的文本放入光标行上
ddp |  交换光标所在行和其下一行(dd剪切当前行，p粘贴当前行的下面)
"(a-z)nyy | 复制n行放入名字为圆括号内的可命名缓冲区，省略n表示当前行
"(a-z)ndd | 删除n行放入名字为圆括号内的可命名缓冲区，省略n表示当前行
"(a-z)p | 将名字为圆括号的可命名缓冲区的内容放入当前行后
"(a-z)P | 将名字为圆括号的可命名缓冲区的内容放入当前行前

## 撤消恢复

| 按键 | 作用 |
| :-: | :-- |
u | 撤消最后一次修改
U | 撤消当前行的所有修改
. | 重复最后一次修改
CTRL+r | 恢复上一次的撤消
"np | 取回最后第n次的删除(缓冲区中存有一定次数的删除内容，一般为9)

## 查找与替换

| 按键 | 作用 |
| :-: | :-- |
/text | 在文件中向前查找text，转义字：.*[]^%/?~$
?text | 在文件中向后查找text
n | 在同一方向重复查找
N | 在相反方向重复查找
fCHAR | 行内向后查找
FCHAR | 行内向前查找
nfCHAR |行内向后查找第三个CHAR
ttext | 在当前行向前查找text，并将光标定位在text的第一个字符
Ttext | 在当前行向后查找text，并将光标定位在text的第一个字符
`*` | 往后查找光标停留位置相同的词组
`#` | 向前查找光标停留位置相同的词组
g* | 向下部分匹配光标所在处的单词
g# | 向上部分匹配光标所在处的单词
`:`set ic | 查找时忽略大小写
`:`set noic | 查找时对大小写敏感
`:`nohlsearch | 关闭当前的高亮显示，如果再次搜索或者按下n或N键，则会再次高亮。
`:`set incsearch | 逐步搜索模式，对当前键入的字符进行搜索而不必等待键入完成。
`:`set wrapscan | 重新搜索，在搜索到文件头或尾时，返回继续搜索，默认开启。
`:`s/OLD/NEW | 用NEW替换OLD，替换当前行的第一个匹配，/可换成%
`:`s/OLD/NEW/g | 用NEW替换OLD，替换当前行的所有匹配
`:`m,ns/OLD/NEW | 在m到n行，用NEW替换OLD,“. ,$” ：从当前行到文件尾
`:`%s/OLD/NEW | 全文用NEW替换OLD，替换所有行的第一个匹配
`:`%s/OLD/NEW/g | 全文替换指定字符串,将g改为c，就会询问是否替换,p 表示替代结果逐行显示
& | 重复最后的`:`s命令
`:`g/text1/s/text2/text3 | 查找包含text1的行，用text3替换text2
`:`g/text/command | 在所有包含text的行运行command所表示的命令
`:`v/text/command | 在所有不包含text的行运行command所表示的命令

## 重复

| 按键 | 作用 |
| :-: | :-- |
, | 以相反的方向重复前面的f、F、t或T查找命令
; | 重复前面的f、F、t或T查找命令
n | 重复前面的/或?查找命令
N | 以相反方向重复前面的/或?命令

## 保存和退出

| 按键 | 作用 |
| :-: | :-- |
`:`w | 保存不退出
`:`w！ | 强制保存不退出
`:`w file | 将修改保存为file不退出
`:`wq或ZZ或:x | 保存文件并退出vi
`:`wq! | 强行保存退出
`:`wqa | 保存所有文件
`:`q!或ZQ | 不保存文件，退出vi
`:`e | 加载最新文件内容
`:`e file | 把指定文件载入vi 进行编辑
`:`e! | 放弃所有修改，从上次保存文件开始再编辑

## vi中的选项

| 按键 | 作用 |
| :-: | :-- |
`:`set all | 打印所有选项
`:`set nooption | 关闭option选项
`:`set nu | 每行前打印行号
`:`set showmode | 显示是输入模式还是替换模式
`:`set noic | 查找时忽略大小写
`:`set list | 显示制表符(^I)和行尾符号
`:`set ts=8 | 为文本输入设置tab stops
`:`set window=n | 设置文本窗口显示n行

## vi命令

| 按键 | 作用 |
| :-: | :-- |
`:`.= | 打印当前行的行号
`:`= | 打印文件中的行数
`:`l | 使用字母"l"来显示许多的特殊字符，如制表符和换行符

## 在文本中定位段落和放置标记

| 按键 | 作用 |
| :-: | :-- |
{ | 在第一列插入{来定义一个段落
[[ | 回到段落的开头处
]] | 向前移到下一个段落的开头处
m(a-z) | 用一个字母来标记当前位置，如用mz表示标记z
'(a-z) | 将光标移动到指定的标记，如用'z表示移动到z

## 在vi中连接行

| 按键 | 作用 |
| :-: | :-- |
J | 将下一行连接到当前行的末尾
nJ | 连接后面n行

## vi中的shell转义命令

| 按键 | 作用 |
| :-: | :-- |
`:`!command | 执行shell的command命令，如:!ls
`:`!! | 执行前一个shell命令
`:`r!command | 读取command命令的输入并插入，如:r!ls会先执行ls，然后读入内容
`:`w!command | 将当前已编辑文件作为command命令的标准输入并执行command命令，如:w!grep all
`:`cd directory | 将当前工作目录更改为directory所表示的目录
`:`sh | 将启动一个子shell，使用^d(ctrl+d)返回vi
`:`so file | 在shell程序file中读入和执行命令

## vi中的宏与缩写

(避免使用控制键和符号，不要使用字符K、V、g、q、v、*、=和功能键)  

| 按键 | 作用 |
| :-: | :-- |
`:`map key commands | 定义一个键来运行commands，如:map e ea，可以用e移到一个字的末尾来追加文本
`:`map | 在状态行显示所有已定义的宏
`:`umap key | 删除该键的宏
`:`ab string1 string2 | 定义一个缩写，使得当插入string1时，用string2替换string1。当要插入文本时，键入string1然后按Esc键，系统就插入了string2
`:`ab | 显示所有缩写
`:`una string | 取消string的缩写

## 在vi中缩进文本

| 按键 | 作用 |
| :-: | :-- |
CTRL+i或tab | 插入模式，插入移动的宽度，移动宽度是事先定义好的
`:`set ai | 打开自动缩进
`:`set sw=n | 将移动宽度设置为n个字符
n<<或>n>> | 使往下n行都向左（右）移动一个设定宽度
== | 自动缩进当前行
: cd C:\Users\Hello\Desktop | 切换目录

## vim配置

### vimrc

windows下，打开gvim,使用`:vi $vim/_vimrc`打开配置文件
linux下，使用`vi ~/.vimrc`打开配置文件

```#!txt
set nocompatible            "不要使用vi的键盘模式，而是vim自己的
set gfn=Consolas:h12            "字体，大小
set nu            "显示行号
set list            "显示TAB
set cursorline            "突出显示当前行"为光标所在行加下划线
set encoding=utf-8            "编码
set fileencodings=uft-8,gbk            "使用utf-8或gbk打开文件
filetype on            "侦测文件类型

set shortmess=atI            "不进入默认首页
set showcmd            "显示命令行

"set backup            "保留备份文件
"set backupdir=$VIM/backup/            "保存备份到backup
set nobackup            "不保留备份文件
set noundofile            "不保留un~文件
set noswapfile            "不生成swap文件

set ruler            "打开状态栏标尺
set laststatus=2            "总是显示状态行
set showtabline=1            "标签栏的显示，0永远不显示 1两个以上显示 2 永远显示
set statusline=%F%m%r%h%w\[POS=%l,%v][%p%%]\%{strftime(\"%d/%m/%y\ -\ %H:%M\")}   "我的状态行显示的内容（包括文件类型和解码）

set nowrapscan            "禁止在搜索到文件两端时重新搜索
set incsearch            "输入搜索内容时就显示搜索结果
set ignorecase            "检索时忽略大小写
set hlsearch            "搜索时高亮显示被找到的文本

set autoread            "当文件在外部被修改时，自动重新读取

colorscheme desert            "设定配色方案
syntax enable            "打开格式设置
syntax on            "自动语法高亮

set ai            "自动缩进
set showmatch            "代码匹配"高亮显示匹配的括号
set matchtime=5            "匹配括号高亮的时间（单位是十分之一秒）

set expandtab            "4个空格代替tab
set softtabstop=4            "统一缩进长度为4
set shiftwidth=4            "自动缩进长度为4
set tabstop=4            "设定 tab 长度为4

set helplang=cn            "帮助系统设置为中文

"set nowrap            "不要换行

set foldmethod=syntax            "代码折叠
set fdm=indent            "代码折叠
set foldlevel=100            "启动vim时不要自动折叠代码
nnoremap <space> zo            "代码折叠快捷键

set formatoptions=tcrqn            "自动格式化
set autoindent            "继承前一行的缩进方式，特别适用于多行注释
set smartindent            "为C程序提供自动缩进
set cindent            "使用C样式的缩进
set smarttab            "在行和段开始处使用制表符

set scrolloff=1            "光标移动到buffer的顶部和底部时保持n行距离
set novisualbell            "不要闪烁

set report=0            "通过使用: commands命令，告诉我们文件的哪一行被改变过
set noerrorbells            "不让vim发出滴滴声
set fillchars=vert:\ ,stl:\            "在被分割的窗口间显示空白，便于阅读 ,stlnc:加了这个wm分割兰有\\
set mouse=a            "可以在buffer的任何地方使用鼠标（类似office中在工作区双击鼠标定位）
set selection=exclusive            "选择模式为单独
set selectmode=mouse,key            "选择方式为鼠标键盘

set viminfo+=!            "保存全局变量
set history=300            "history文件中需要记录的行数

set magic            "设置正表达式
set backspace=indent,eol,start  "这指明在插入模式下在哪里允许 <BS> 删除光标前面的字符"逗号分隔的三个值分别指：行首的空白字符，换行符和插入模式开始处之前的字符。

let Tlist_Show_One_File=1    "不同时显示多个文件的tag，只显示当前文件的
let Tlist_Exit_OnlyWindow=1    "如果taglist窗口是最后一个窗口,则退出vim
let autosave=15            "15s,自动保存文件

au BufRead,BufNewFile,BufEnter * cd %:p:h "自动切换目录为当前编辑文件所在目录
"保存到指定文档
if has(isdirectory('$HOME\Desktop\'))
    exec 'cd ' . fnameescape('$HOME\Desktop\')

if has("gui_running")            "如果是图形界面
    set guioptions=m            "关闭菜单栏
    set guioptions=t            "关闭工具栏
"    set guioptions=L            "启动左边的滚动条
"    set guioptions+=r            "启动右边的滚动条
"    set guioptions+=b            "启动下边的滚动条
    set clipboard+=unnamed            "共享剪贴板
endif
"if has("win32")
"    colorscheme torte    "torte配色方案
"    set guifont=Consolas:h12 "字体和大小
"endif

"--------------end self config-------------------
```

自动打开上一个文本

```#!txt
"Go to last file(s) if invoked without arguments.
autocmd VimLeave * nested if (!isdirectory($HOME . "/.vim")) |
    \ call mkdir($HOME . "/.vim") |
    \ endif |
    \ execute "mksession! ". $HOME . "/.vim/Session.vim"

autocmd VimEnter * nested if argc() == 0 && filereadable($HOME . "/.vim/Session.vim") |
    \ execute "source ". $HOME . "/.vim/Session.vim"
```

文件管理器设置

```#!txt
"MiniBufExplorer
let g:miniBufExplMapWindowNavVim = 1
let g:miniBufExplMapWindowNavArrows = 1
let g:miniBufExplMapCTabSwitchBufs = 1
let g:miniBufExplModSelTarget = 1
```

## gvim不生成备份文件

打开vimrc_example.vim文件，找到下面的代码：

    ```#!txt
    if has("vms")
        set nobackup "do not keep a backup file, use versions instead
    else
        set backup "keep a backup file
    endif
    ```

注释掉else后面的内容