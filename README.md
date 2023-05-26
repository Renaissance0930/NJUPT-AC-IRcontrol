# NJUPT-AC-IRcontrol
南邮空调遥控
=====
## 项目背景：<br>
寝室4个人每个人都想调空调，空调遥控器要么在床下不想下床，要么在别人床上找不到，极低成本实现(不带红外的)手机远程控制<br>
本实验基于Mixiaoxiao开发的固件进行简化适配[项目地址](https://github.com/Mixiaoxiao/ESP8266-IR-HOMEKIT)<br>
## 材料准备：<br>
esp8266开发板---10r<br>
红外二极管----0.2r<br>
红外接收管(可选)<br>
## *提示：*
有条件的寝室最好自己带一个路由器，校园网环境复杂，和开发板不在一个子网内不是很方便<br>
## 硬件连线
只需要使用两根杜邦线将红外二极管的正极接在ESP8266的`D5`(GPIO.14)脚，负极接`GND` (有接三极管放大电路的接法，但是直接接也能用，就不搞复杂了)，如图：<br>
![](https://github.com/Renaissance0930/NJUPT-AC-IRcontrol/blob/main/%E6%8E%A5%E7%BA%BF.png)<br>
PS:二极管长脚为正，短脚为负<br>
## 基本操作
### 1、环境初始配置<br>
拿到板子后用数据线连接电脑，准备刷写固件<br>
这里使用esphome-flasher进行刷写固件<br>
工具可以用项目包中的文件，也可以通过[下载地址](https://github.com/esphome/esphome-flasher/releases/download/1.4.0/ESPHome-Flasher-1.4.0-Windows-x64.exe)下载<br>
软件界面：<br>
![](https://github.com/Renaissance0930/NJUPT-AC-IRcontrol/blob/main/%E5%9B%BE%E7%89%871.png)<br>
在*serial port*处选择端口(正常就一个选项)
*Firmware*选择项目文件目录中的`1.bin`文件，点击*FlashESP*进行烧写<br>
等待输出打印烧写成功，进入下一步操作<br>
### 2、网络环境配置<br>
在固件烧写成功后，ESP8266会自动生成一个SSID为`ESP_CONFIG_XXXXXX`的WiFi热点，使用手机连接后会自动弹出配网界面，如果未自动弹出浏览器输入`192.168.4.1`也可手动进入<br>
配置界面如下<br>
![](https://github.com/Renaissance0930/NJUPT-AC-IRcontrol/blob/main/%E5%9B%BE%E7%89%872.png)<br>
比如这里我选择`世界最高城-理塘`，输入WiFi密码后，点击发送WIFI配置信息即可完成配网<br>
根据配网界面连接好网络后，开发板上的LED将会熄灭，此时用手机再次连接刚刚给开发板配置的WiFi，在浏览器输入IP地址`192.168.1.66`即可进入空调遥控界面<br>
![](https://github.com/Renaissance0930/NJUPT-AC-IRcontrol/blob/main/%E5%9B%BE%E7%89%873.png)<br>
### 3、实现遥控
在控制界面设置空调配置，协议处选择空调的品牌，比如我们寝室是格力的空调，在协议处选择`GREE`<br>
在下方空调基础配置里选择好控制选项，点击发射红外即可实现对空调的控制<br>
## 进阶操作
### 1、连接Homekit，接入苹果生态实现Siri控制<br>
(1)打开iPhone或iPad上的`家庭`软件<br>
(2)点击右上角'＋'号，选择`添加配件`<br>
(3)点击`其他选项`或`我没有或无法扫描代码`，手机会自动搜索附近的家庭设备<br>
(4)选择弹出的遥控器，选择信任未认证的配件，输入设置代码`11111111`<br>
(5)等待手机自动配置即可，稍后遥控器会出现在家庭APP中，可以在家庭APP中直接控制空调<br>
![](https://github.com/Renaissance0930/NJUPT-AC-IRcontrol/blob/main/%E5%9B%BE%E7%89%874.png)<br>
## 以下较为复杂，涉及操作较多，有需要后期专门开一个项目详细讲
### 2、连接homeassistant，与更多设备联动并实现根据温度变化自动开空调<br>
### 3、映射到公网，实现远程操控，比如当下酷暑难耐，人在教学楼提前打开寝室空调等
