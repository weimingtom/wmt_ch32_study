# wmt_ch32_study
My study of wch ch32f103 and ch32v103

## 感想1, ch32f103
最近无聊去研究wch（沁恒）的ch32单片机，  
这家公司就是经常听到的usb转串口的ch340那家公司。  
起因是我本来想买ch32v103r8t6的开发板，  
结果买成了ch32f103r8t6，所以就顺便研究一下。  
实际上价格上跟m3架构的stm32没太大差别（都涨价了），  
但可能比gd32要便宜一点。特点是支持husb烧录，  
但前提是开发板支持，否则最好还是用串口烧录  

## 感想2, ch32v103  
源地工作室的ch32v103r8t6和ch32v103c8t6到手了（注意区分v103和f103，很容易弄混）。  
源地工作室的版本，两个板的灯都是PC13，烧录则建议用wch-link（避免长按BOOT0按钮重启），  
支持断点和烧录（如果是f103的话，需要换其他烧录器和调试器，如果硬来的话会报错）。  
这里需要小心几点：烧录地址要选第一个，否则烧录后无法运行；不可以烧录f103的hex固件文件，  
因为架构不同不兼容；usb口可能不支持husb烧录，可以尝试串口烧录或者wch-link烧录

## 感想3, MounRiver Studio  
总体来说，结合wch-link的使用（仅限于RISC-V版的ch32v103系列单片机），  
MounRiver Studio的威力可以达到极致（不过也支持ARM架构），  
已经很接近于keil 5的效果（当然，stm32cubemx的代码生成功能的威力仍旧没办法匹敌）。  
如果喜欢断点的话可以选择ch32v103。按道理gd32vf103也可以做到这点，  
不过MounRiver Studio也支持gd32vf103，所以自己按需选择了  

## WCH-Link烧录, 源地工作室, ch32v103r8t6, ch32v103c8t6  
注意程序地址选第一个  
3.3  
DIO  
CLK  
GND  
闪烁灯  
PC13  
兼容CH32V103C8T6  

## WCH-Link 相关资料汇总及技术支持BBS:  
【链接：】 http://wch.cn/bbs/thread-71088-1.htmlCH32V103 数据手册：CH32V103DS0.PDF   
【下载链接：】 http://wch.cn/downloads/CH32V103DS0_PDF.html   
CH32V103用户手册：CH32xRM.PDF  
【下载链接：】 http://wch.cn/downloads/CH32xRM_PDF.html   
 CH32V103官方例程：CH32V103EVT.ZIP  
【下载链接：】 http://wch.cn/downloads/CH32V103EVT_ZIP.html   
MounRiver Studio（MRS）：  
【下载链接：】 http://mounriver.com/    

## 串口烧录, ch32f103   
Rxd——>A9  
Txd---->A10  
GND——>G  
VCC——>3.3  

## HUSB下载（不用额外的下载器，数据线就可以下载）, ch32f103    
CH32F103有2个USB口，一个是主机usb，一个是设备usb。分别对应的管脚为：
HUSB：  
PB7------>D+  
PB6------>D-  
USB：  
PA12----->D+  
PA11----->D-  

## ch32f103, usb烧录    
http://www.wch.cn/downloads/CH32F103DS0_PDF.html  
* 烧录态：  
BOOT0<->VCC（杜邦线）（左1列倒2行，左2列倒3行）  
BOOT1<->GND（跳帽）（左1列倒1行，左2列倒1行）  
PA0<->LED1（杜邦线）（左1列4行，右1列1行）  
P_HUSB1<->PC（如果接上，驱动正确，WCHISPTool会自动显示出设备）  
* WCHISPTool：  
选择32位 CH32F10X  
取消启动读保护勾选  
用户程序文件*.hex  
点击下载按钮  
* 运行态：  
BOOT0<->GND（跳帽）（左1列倒2行，左2列倒2行）  
BOOT1（悬空）  
PA0<->LED1（杜邦线，闪烁蓝灯）（左1列4行，右1列1行）  
P_USB<->S2 Left (开关向左，接通电源）D1红灯   
