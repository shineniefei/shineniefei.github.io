---
title: selenium python
---

# selenium python

## 介绍

## 启动

```
#!/usr/bin/env python3
# coding:utf-8

import os
import sys

try:
    # 配置目录
    from conf.selenium_config import RESPATH
    os.path.exists(RESPATH)
except:
    # 本机目录，末尾不加 “/”
    RESPATH = 'D:/IDE/Test/res'
    if os.path.exists(RESPATH) is False:
        print(RESPATH, ' is not find')
        quit()

from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
from selenium.webdriver.firefox.firefox_binary import FirefoxBinary


def chromeDriver():
    driverPath = RESPATH + "/chromedriver2.31.exe"
    # chrome.exe地址
    chromePath = RESPATH + "/Chrome60/chrome.exe"
    # chrome启动选项
    options = webdriver.ChromeOptions()
    # options.add_argument("--user-data-dir=" + chromeoptionPath))
    options.add_argument("--start-maximized")
    options.add_argument("--test-type")
    options.add_argument("allow-running-insecure-content")
    if os.path.isfile(chromePath):
        options.binary_location = chromePath
    # 带参数启动driver
    dr = webdriver.Chrome(
        chrome_options=options, executable_path=driverPath, port=9515)
    dr.implicitly_wait(10)  # 隐性等待，最长等10秒
    print('driver started')
    return dr


def firefoxDriver():
    # 获取当前文件夹的绝对路径#driver地址
    ffpath = RESPATH + "/Mozilla Firefox46/firefox.exe"
    binary = FirefoxBinary(ffpath)
    # 带参数启动driver
    # profile = webdriver.FirefoxProfile(xx)
    if os.path.isfile(ffpath):
        dr = webdriver.Firefox(firefox_binary=binary)
    else:
        dr = webdriver.Firefox()
    # 将浏览器最大化
    dr.maximize_window()
    # 隐性等待，最长等10秒
    dr.implicitly_wait(10)
    print('driver started')
    return dr


def ieDriver():
    # 修改配置信息
    DesiredCapabilities.INTERNETEXPLORER['ignoreProtectedModeSettings'] = True
    # 获取当前文件夹的绝对路径+driver地址
    driverPath = RESPATH + "/IEDriverServer_x64_2.53.1.exe"
    dr = webdriver.Ie(executable_path=driverPath)
    # 将浏览器最大化
    dr.maximize_window()
    # 隐性等待，最长等10秒
    dr.implicitly_wait(10)
    print('driver started')
    return dr


if __name__ == '__main__':
    # chromeDriver()
    # firefoxDriver()
    ieDriver()
```

## 元素定位

定位元素先要掌握基本的HTML语法：

1. 定位单个元素

  ```
  find_element_by_id('selenium')                      #通过id方式定位 
  find_element_by_name('selenium')                    #通过name方式定位 
  find_element_by_class_name('selenium')              #通过class name 方式定位
  find_element_by_tag_name('selenium')                #通过tag name方式定位 
  find_element_by_link_text('selenium')               #通过text方式定位
  find_element_by_partial_link_text('selenium')       #通过部分text方式定位
  find_element_by_xpath('//input[@id="selenium"]')    #通过xpath方式定位
  find_element_by_css_selector('selenium')            #通过CSS方式定位
  ```

2. 定位一组元素,批量对象（复选框）复选框

  ```
  find_element_by_id('selenium')                  
  find_element_by_name('selenium')                
  find_element_by_class_name('selenium')          
  find_element_by_tag_name('selenium')            
  find_element_by_link_text('selenium')           
  find_element_by_partial_link_text('selenium')   
  find_element_by_xpath('//input[@id="selenium"]')
  find_element_by_css_selector("[ value='百度一下']")
  ```

3. 相同属性的元素一组对象，取对应的第几个

  ```
  find_element_by_id('selenium')[1]                  
  find_element_by_name('selenium')[1]                
  find_element_by_class_name('selenium')[1]          
  find_element_by_tag_name('selenium')[1]            
  find_element_by_link_text('selenium')[1]           
  find_element_by_partial_link_text('selenium')[1]   
  find_element_by_xpath('//input[@id="selenium"]')[1]
  find_element_by_css_selector('selenium')[1]
  ```

  _注意：()和(-1)都表示最后一个元素_ _xpath语法通过firepath插件可以生成，可以直接使用_

4. 高级 ```

  # 层级与属性结合

  find_element_by_xpath("//div[@class='selenium']/input/span") find_element_by_xpath("//div[@class='selenium']/div[2]/input") find_element_by_xpath(.//*[@id='selenium']/../div/div/div[2]/div[4]/button)

# 通过逻辑运算符定位

find_element_by_xpath("//input[@id='selenium' and @class='selenium1']/span/input") find_element_by_css_selector("form#form>span>input#su")

```
1\. 使用starts-with

//div[starts-with(@id,'res')]//table//tr//td[2]//table//tr//td//a//span[contains(.,'Developer Tutorial')]

2\. 使用contains和and

//div[starts-with(@id,'res')]//table[1]//tr//td[2]//a//span[contains(.,'_Test') and contains(.,'KPI')]

3\. 使用descendant

//div[starts-with(@id,'res')]//table[1]//tr//td[2]//a//span[contains(.,'QuickStart')]/../../../descendant::img

4\. 使用ancestor

//div[starts-with(@id,'res')]//table[1]//tr//td[2]//a//span[contains(.,'QuickStart')]/ancestor::div[starts-with(@id,'res')]//table[2]//descendant::a[2]

5\. 使用text()

//span[@id='idHeaderTitleCell' and contains(text(),'QuickStart')]

## 控制

### 浏览器控制  

1\. 控制浏览器大小：
```

driver.set_window_size(400,500)<br>
driver.maximize_window() #无参数

```
浏览器后退、前进：
```

driver.back()-后退、 driver.farward()-前进

```
### 多表单切换（有frame嵌套表单）
```

dr.switch_to_frame("frameid")#通过frame的id进入iframe<br>
dr.switch_to_frame("frameName") #通过frame的name进入iframe

framepath=dr.find_element_by_class_name("frameClassname")<br>
dr.switch_to_frame(framepath)#通过frame页面对象进入iframe

dr.switch_to_default_content()#退出当前frame返回上一层

```
多窗口切换  
selenium-webdriver中使用switch_to_window()方法来切换任意窗口，常用方法有  
driver.current_window_handle    #获取当前窗口句柄  
driver.window_handles            #返回所有窗口句柄到当前会话  
driver.switch_to_window()       #进入窗口，用于切换不同窗口  
dr.title  

警告框处理  
    webdriver中处理js生成的alert、confirm、prompt处理方法是：使用switch_to_alert()定位到alert/confirm/prompt，

alert=dr.switch_to_alert()                    #进入alert  
alert.text #打印对话框里的文字内容  
alert.accept()#对话框里点击alert中确定按钮  
alert.dismiss() #对话框里点击取消按钮  
alert.send_keys("对话框中输入的内容") #在对话框里输入内容  

十二、上传文件  
    分2种：普通上传、插件上传  
    普通上传：将本地文件的路径作为一个值放到input标签中，通过form表单提交时，将值传给服务器中去  
    插件上传：指基于flash、javascript或ajax技术实现的上传功能或插件。  
    1.针对普通上传用send_keys实现  
python代码：  

    dr.get("D:\\workspace\\pySelenium\\resources\\upload.htm")  
    loadFile=dr.find_element_by_name("filebutton")# 获取上传文件input元素节点  
    loadFile.send_keys("D:\\workspace\\pySelenium\\resources\\frame.htm")#输入上传文件地址来实现上传  

    2.插件上传:使用AutoIt实现，--需要安装AutoIt程序  
        AutoIt安装，使用暂时略，需要时再追加，流程为：用AutoIt编写上传文件脚本生成exe文件，在python脚本中进行调用  
python代码：  

    loadFile=dr.find_element_by_name("filebutton")# 获取上传按钮  
    loadFile.click()    #点击上传按钮，弹出上传对话框  
    os.system("D:\\autoItFile.exe")    #调用autoIt生成的exe文件，实现导入  

十三、下载文件:使用AutoIt实现，--需要安装AutoIt程序，方法同上传  
python代码：  

    ffp=webdriver.FirefoxProfile()  
    ffp.set_preference("browser.download.folderList",2)#0:代表下载到浏览器默认路径下；2：下载到指定目录  
    ffp.set_preference("browser.download.manager.showWhenStarting",False)#是否显示开始：True：显示；False：不显示  
    ffp.set_preference("browser.download.dir", os.getcwd())#指定下载文件目录，os.getcwd()无参数，返回当前目录  
    # ffp.set_preference("browser.helperApps.neverAsk.saveToDisk","application/octet-stream")#下载文件类型，  
    #指定下载页面的content-type值，application/octet-stream为文件类型，http-content-type常用对照表搜索百度  
    dr=webdriver.Firefox(firefox_profile=ffp)  
    dr.get("https://pypi.python.org/pypi/selenium#downloads")  
    dr.find_element_by_xpath("//div[@id='content']/div[3]/table/tbody/tr[3]/td[1]/span/a[1]").click()  
    #接下来使用autoIt实现  

十四、cookies操作  
    webdriver操作cookies的方法：  
    get_cookies()：获得所有cookies的值  
    get_cookie(name)：获得有特定name值的cookie信息  
    add_cookie(cookie_dict)：添加cookie，必须有name和value  
    delete_cookie(name)：删除特定名称的cookie信息，通过name找到特定的cookie并删除  
    delete_all_cookies()：删除浏览器中所有cookie的信息  
    注意：1.cookie是以字典形式进行存储的；  
    2.使用场景：如登录功能会把用户名写入浏览器cookie指定key为username，那么就可以通过get_cookies()找到username，打印value，找不到说明保存浏览器的cookie是有bug的。  
python代码：  

    num=1  
    dr.get("http://www.baidu.com")  
    cookies=dr.get_cookies()#获取cookie的所有信息  
    for ck in cookies:  
    print'----所有cookie',num,':',ck #打印cookie的所有信息  
    num=num+1  
    print'----按name查cookie：',dr.get_cookie("PSTM")#通过cookie的name获取cookie信息  
    dr.add_cookie({'name':'hello','value':'123456789'})#向name和value添加会话信息  
    cookies2=dr.get_cookies()#重新获取cookie的所有信息  
    for ck2 in cookies2:  
    if ck2['name']=='hello':  
    print"----加入的cookie信息：%s-->%s",(ck2['name'],ck2['value'])  

十五、javascript调用，python使用的方法：execute_script()  
python代码：  

    dr.get("http://www.baidu.com")  
    dr.find_element_by_id("kw").send_keys("selenium")  
    dr.find_element_by_id("su").click()  
    js="var q=document.documentElement.scrollTop=1000"    #滚动条滚到最下面  
    dr.execute_script(js)  
    time.sleep(4)  
    js2="var q=document.documentElement.scrollTop=0"      #滚动条滚到页面顶  
    dr.execute_script(js2)  

十六、截图，适用于脚本出错时，对当前窗口进行截图保存，使用函数：get_screenshot_as_file()  
python代码：  

    dr.get("http://www.baidu.com")  
    try:  
    dr.find_element_by_id("kw1").send_keys("selenium")  
    dr.find_element_by_id("su").click()  
    exceptNoSuchElementException,msg:  
    dr.get_screenshot_as_file("d:\\error.jpg")    #截图输出到d盘  
    print msg  
    dr.close()  

十七、关闭窗口  
    quit()：退出相关驱动程序并关闭所有窗口。  
    close()：关闭当前窗口，打给多个窗口时，可使用来关闭当前窗口  

## 事件

### 鼠标事件
```

ActionChains类提供的常用方法：<br>
1.1 perform()：执行ActionChains中存储的所有行为,对整个事件进行提交<br>
1.2 context_click(): 右击<br>
如：<br>
from selenium.webdriver.common.action_chains import ActionChains<br>
...<br>
ActionChains(dr).context_click(docfile).perform()<br>
1.3 double_click(): 双击<br>
如：<br>
from selenium.webdriver.common.action_chains import ActionChains<br>
...<br>
doubleClick=dr.find_element_by_id("xxx")<br>
ActionChains(dr). double_Click(doubleClick).perform()<br>
1.4 drag_and_drop(source,target): 拖动<br>
如：<br>
from selenium.webdriver.common.action_chains import ActionChains<br>
...<br>
dsource=dr.find_element_by_id("xxx") #拖动的源元素<br>
dtarget=dr.find_element_by_id("xxx") #释放的目标目标元素<br>
ActionChains(dr).drag_and_drop(dsource,dtarget).perform()<br>
1.5 move_to_element(): 鼠标悬停<br>
如：<br>
from selenium.webdriver.common.action_chains import ActionChains<br>
...<br>
above=dr.find_element_by_id("xxx")<br>
ActionChains(dr).move_to_element(above).perform()

```
### 键盘事件
```

```
from selenium.webdriver.common.keys importKeys  
...  
dr.get("http://www.baidu.com")  
#输入内容  
dr.find_element_by_id("kw").send_keys("seleniumm")  
#删除输入内容的最后一个字母,  
dr.find_element_by_id("kw").send_keys(Keys.BACK_SPACE)  
#输入：空格+教程  
dr.find_element_by_id("kw").send_keys(Keys.SPACE)  
dr.find_element_by_id("kw").send_keys(u"教程")  
#ctrl+a全选输入框内容  
dr.find_element_by_id("kw").send_keys(Keys.CONTROL,'a')  
#ctrl+x剪贴输入框内容  
dr.find_element_by_id("kw").send_keys(Keys.CONTROL,'x')  
#ctrl+v剪贴输入框内容  
dr.find_element_by_id("kw").send_keys(Keys.CONTROL,'v')  
#回车键操作  
dr.find_element_by_id("su").send_keys(Keys.ENTER)  
dr.close()  

常用的键盘操作整理：  
send_keys(Keys.BACK_SPACE)  #删除键BackSpace  
send_keys(Keys.SPACE)       #空格键Space  
send_keys(Keys.TAB)         #制表键Tab  
send_keys(Keys.ESCAPE)      #回退键Esc  
send_keys(Keys.ENTER)       #回车键Enter  
send_keys(Keys.CONTROL,'a') #Ctrl+a  
send_keys(Keys.CONTROL,'c') #Ctrl+c      
send_keys(Keys.CONTROL,'x') #Ctrl+x  
send_keys(Keys.CONTROL,'v') #Ctrl+x  
send_keys(Keys.F1)          #F1,类似的有F1-F12
```

```
## 动作

## 等待

### 显示等待
```

WebDriverWait(driver, timeout,poll_frequency,ignored_exceptions=None).until(method,message)<br>
示例：<br>
WebDriverWait(dr,5,0.5,None).until(<br>
expected_conditions.presence_of_element_located((By.ID,"kw1")),message='test')<br>
解释：<br>
A.WebDriverWait()：在设置时间内，默认间隔一段时间检测一次当前页面元素是否存在，若超过当前指定时间检测不到则抛出异常；<br>
B.driver：webdriver的浏览器驱动，ie、firefox、chromea<br>
C.timeout：最长超时时间，以秒为单位<br>
D.poll_frequency：休眠间隔时间-步长，默认0.5秒<br>
E.ignored_exceptions：超时后异常信息，默认抛出NoSuchElementException异常<br>
F.until(method,message): 调用该方法提供的驱动作为一个参数，直到返回值为True<br>
G.until_not(method,message):调用该方法提供的驱动作为一个参数，直到返回值为False<br>
H.expected_conditions类提供的预期条件实现有：<br>
title_is:判断标题是否是xx<br>
title_contains:判断标题是否包含xx<br>
presence_of_element_located：元素是否存在

```
visibility_of_element_located：元素是否存在  

    visibility_of：是否可见  

    presence_of_all_elements_located：判断一组元素是否存在  

    text_to_be_present_in_element：判断元素是否有xx文本信息    

    text_to_be_present_in_element_value：判断元素值是否有xx文本信息    

    frame_to_be_available_and_switch_to_it：表单是否可见，并切换到该表单  

    invisibility_of_element_located：判断元素是否隐藏  
    element_to_be_clickable：判断元素是否点击，它处于可见和启动状态  
    staleness_of：等到一个元素不再依附于DOM  
    element_to_be_selected：被选中的元素  
    element_located_to_be_selected：一个期望的元素位于被选中  
    element_selection_state_to_be：一个期望检查如果给定元素被选中  
    element_located_selection_state_to_be：期望找到一个元素并检查是否是选择状态  
    alert_is_present：预期一个警告信息
```

```
### 隐式等待:

通过一定的时长等待页面所有元素加载完成，哪个元素超出设置时长没被加载就抛出异常NoSuchElementException，隐式等待是针对所有元素的
```

```
implicitly_wait(5)    #默认单位为秒  
示例：  
    dr.implicitly_wait(5)
```

```
### sleep休眠

python中强制的程序等待
```

```
time.sleep(4)    #默认单位秒，设置小于1秒的时间可以用小数点如sleep(0.6)
```

```
## 问题

### 验证码处理  

    方法1：去掉验证码
    方法2：设置万能验证码
    方法3：使用cookie方法获取，cookie时间延长

### 截屏
```

```
driver.save_screenshot('E:\\pythonScript\\images\\'+time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())+'baidu.png')
```

```
## Element取值
```

size 获取元素的尺寸<br>
text 获取元素的文本<br>
get_attribute(name) 获取属性值<br>
location 获取元素坐标，先找到要获取的元素，再调用该方法<br>
page_source 返回页面源码<br>
driver.title 返回页面标题<br>
current_url 获取当前页面的URL<br>
is_displayed() 设置该元素是否可见<br>
is_enabled() 判断元素是否被使用<br>
is_selected() 判断元素是否被选中<br>
tag_name 返回元素的tagName ```

## 常用函数

1.获取当前页面的Url函数<br>
driver.current_url

2.获取元素坐标<br>
driver.find_element_by_id('selenium').location

3.表单的提交<br>
driver.find_element_by_id('selenium').submit()

4.获取CSS的属性值<br>
driver.find_element_by_css_selector("input.btn").value_of_css_property("input.btn")

5.获取元素的属性值<br>
driver.find_element_by_id('selenium').get_attribute("selenium")

6.判断元素是否被选中<br>
driver.find_element_by_id("form1").is_selected()

7.返回元素的大小<br>
driver.find_element_by_id("iptPassword").size<br>
//返回值：{'width': 250, 'height': 30}

8.判断元素是否显示<br>
driver.find_element_by_id("iptPassword").is_displayed()

9.判断元素是否被使用<br>
driver.find_element_by_id("iptPassword").is_enabled()

10.获取元素的文本值 driver.find_element_by_id("iptUsername").text

11.元素赋值<br>
driver.find_element_by_id("iptUsername").send_keys('admin')

12.返回元素的tagName<br>
driver.find_element_by_id("iptUsername").tag_name

13.删除浏览器所有的cookies<br>
driver.delete_all_cookies()

14.删除指定的cookie<br>
deriver.delete_cookie("my_cookie_name")

15.关闭浏览器<br>
driver.close()

16.关闭浏览器并且推出驱动程序<br>
driver.quit()

17.返回上一页<br>
driver.back()

18.设置等待超时<br>
driver.implicitly_wait(30)

19.浏览器窗口最大化<br>
driver.maximize_window()

20.查看浏览器的名字<br>
drvier.name

## selenium版本进行降级

降级方法如下：

1)查看当前的selenium版本打开终端，输入 pip show selenium python3 -m pip show selenium python2.7 -m pip show selenium 2）删除当前python下的selenium版本为了避免与之前安装的selenium版本冲突，先找到selenium3.0目录：python\Lib\site-packages目录把里面selenium开头的文件全部删除就可以了。python所有的第三方包都在这个目录下面。selenium相关的目录全部删除。 3）打开终端，输入 pip install selenium==2.53.6 （注意是两个==，中间不要留空格，这里推荐2.53.6的版本） python3 pip install selenium==2.53.6 python2.7 pip install selenium==2.53.6

## IE报错

File "D:\goodgoodstudy\Python35\lib\site-packages\selenium\webdriver\remote\webdriver.py", line 248, in get self.execute(Command.GET, {'url': url}) File "D:\goodgoodstudy\Python35\lib\site-packages\selenium\webdriver\remote\webdriver.py", line 236, in execute self.error_handler.check_response(response) File "D:\goodgoodstudy\Python35\lib\site-packages\selenium\webdriver\remote\errorhandler.py", line 192, in check_response raise exception_class(message, screen, stacktrace) selenium.common.exceptions.WebDriverException: Message: Failed to navigate to <https://www.baidu.com>. This usually means that a call to the COM method IWebBrowser2::Navigate2() failed.

该错误是需要在DCOM组件服务器中给Internet Explorer授权。操作如下： （1）打开开始菜单的运行对话框，输入dcomcnfg命令，确定，这时会弹出组件服务窗口 （2）展开计算机-〉我的电脑-〉DCOM配置，找到Internet Explorer应用程序节点 （3）单击右键-〉属性，选中"安全"选项，在下面三个项目都选择"自定义"，并单击编辑按钮 （4）在启动权限对话框中查看用户权限，全部给到最大权限。 （5） 选择"身份标识",再选择"交互式用户"即可

以上完美解决了能打开浏览器但是一直不能获取到地址的问题。 from selenium.webdriver.common.desired_capabilities import DesiredCapabilities DesiredCapabilities.INTERNETEXPLORER['ignoreProtectedModeSettings'] = True

System.setProperty("webdriver.chrome.driver", "files/chromedriver.exe"); ChromeOptions options = new ChromeOptions(); options.setBinary("C:/Chrome/Application/chrome.exe"); ChromeDriver driver = new ChromeDriver(options);
