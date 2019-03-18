---
title: vimium
---

# Vimium Help

|command|en|cn|
|:-:|:--|:--|
Navigating the page|---|---
j, `<`c-e> | Scroll down |向下移动（CTRL+e）
k, `<`c-y> | Scroll up |向上移动（CTRL+y）
gg | Scroll to the top of the page |跳到页面顶部
G | Scroll to the bottom of the page |跳到页面底部
d | Scroll a half page down |向下翻页
u | Scroll a half page up |向上翻页
h | Scroll left |向左移动
l | Scroll right |向右移动
zH | Scroll all the way to the left |移动到最左
zL | Scroll all the way to the right |移动到最右
r | Reload the page |刷新页面
yy | Copy the current URL to the clipboard |拷贝当前页面的URL到剪贴板
p | Open the clipboard's URL in the current tab |在当前页打开剪贴板的地址
P | Open the clipboard's URL in a new tab |在新页面打开剪贴板的地址
gu | Go up the URL hierarchy |跳转到父页面（url往上一个/）
gU | Go to root of current URL hierarchy |跳转到根页面（url的hosts一级）
i | Enter insert mode |插入模式
v | Enter visual mode |可视模式
V | Enter visual line mode |行可视模式
gi | Focus the first text input on the page |到第一个文本框插入
f | Open a link in the current tab |Hint模式，在本页面打开待选择的链接
F | Open a link in a new tab |Hint模式，在新页面打开待选择的链接
`<`a-f> | Open multiple links in a new tab |Hint模式，在新页面打开待选择的多个链接（ALT+f）
yf | Copy a link URL to the clipboard |拷贝某一个URL到剪贴板（y拷f选择，选择后生效）
[[ | Follow the link labeled previous or < |转到当前页之前标记的链接
]] | Follow the link labeled next or > |转到当前页之后标记的链接
gf | Select the next frame on the page |到当前页面的下一层框架
gF | Select the page's main/top frame |到当前页面的最上层框架
m | Create a new mark |创建一个标记（按下后，接一个字母）
` | Go to a mark  |跳到一个标记（按下后，接用m标记过的字母）
|**Using the vomnibar**|
o | Open URL, bookmark or history entry |在当前页打开网址，书签，历史记录
O | Open URL, bookmark or history entry in a new tab |在新页面打开网址，书签，历史记录
b | Open a bookmark |在当前页打开书签
B | Open a bookmark in a new tab |在新的标签页打开书签
T | Search through your open tabs |在所有打开的标签页查找跳转
ge | Edit the current URL |编辑当前地址，回车在本页面打开
gE | Edit the current URL and open in a new tab |编辑当前地址，回车在新页面打开
|**Using find**|
/ | Enter find mode |查找
n | Cycle forward to the next find match |向下查找内容
N | Cycle backward to the previous find match |向上查找内容
|**Navigating history**|
H | Go back in history |退到上一个历史页面
L | Go forward in history |进到下一个历史页面
|**Manipulating tabs**|
t | Create new tab |创建一个新的标签页
J, gT | Go one tab left |跳转到右边的一个标签页
K, gt | Go one tab right |跳转到右边的一个标签页
^ | Go to previously-visited tab |切换到之前浏览在窗口
g0 | Go to the first tab |移动到第一个标签页
g$ | Go to the last tab |移动到最后一个标签页
yt | Duplicate current tab |复制当前页到新标签页
`<`a-p> | Pin or unpin current tab |使当前页的标签最小化（再按还原）
`<`a-m> | Mute or unmute current tab |使当前页静音（再按取消静音）
x | Close current tab |关闭当前的标签页
X | Restore closed tab |恢复刚刚关闭的标签页
W | Move tab to new window |移动标签页到新窗口
<< | Move tab to the left |往左移动标签页
`>`> | Move tab to the right |往右移动标签页
|**Miscellaneous**|
? | Show help |显示命令帮助（再按关闭）
gs | View page source|查看页面源代码

F6定位并选择地址栏  