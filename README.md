# Hijacker

Hijacker是用于渗透测试工具的图形用户界面[Aircrack-ng, Airodump-ng](https://www.aircrack-ng.org/)，[MDK3](https://tools.kali.org/wireless-attacks/mdk3)和[Reaver](https://tools.kali.org/wireless-attacks/reaver)。它提供了一个简单易用的UI来使用这些工具，而无需在控制台中键入命令并复制和粘贴MAC地址。

此应用程序需要具有支持**监视器模式**的内部无线适配器的**ARM**架构的android设备。少数android设备可以使用，但本机都不能使用。这意味着您将需要自定义固件。任何使用BCM4339芯片组（MSM8974，例如Nexus 5，Xperia Z1/Z2，LG G2，LG G Flex，三星Galaxy Note 3）的设备都可以与[Nexmon](https://github.com/seemoo-lab/nexmon) (它还支持其他一些芯片组)一起使用  will work with。使用BCM4330的设备可以使用[bcmon](http://bcmon.blogspot.gr/).

一种替代方法是利用OTG数据线在Android设备上使用支持**监视模式**的外部适配器。

所需的工具包含在**ARM**设备中。
还包括用于**BCM4339**和**BCM4358**的Nexmon固件和管理实用程序。

root权限访问也是必要的，因为这些工具需要root权限才能工作。

## 已停止维护
由于目前正在开发一个全新的迭代，因此该应用已停止使用。由于新版本将长期不可用，因此此回购协议仍处于开放状态，以征求建议和功能要求，这些建议和功能要求将在新版本中实现。可能仍会提供关键的更改，以及有关构建，维护和更新代码的帮助（尽管我不推荐）。只要来自最新发布的版本，错误报告也将受到欢迎，因为某些代码可能会在新项目中使用。


## 特色
### 信息收集
* 查看您附近（甚至是隐藏的）访问点和站点（客户端）的列表
* 查看特定网络（通过测量信标和数据包）及其客户端的活动
* 有关接入点和站点的统计信息
* 从OUI数据库中查看设备（AP或工作站）的制造商
* 查看设备的信号功率并过滤距离您最近的设备
* 将捕获的数据包保存在.cap文件中

### 攻击
* **取消**对网络中所有客户端的身份验证（针对每个客户端（有效）或不指定特定目标）
* 从连接的网络上取消对特定客户端的身份验证
* 带有自定义选项和SSID列表的MDK3 **Beacon Flooding**
* 针对特定网络或附近每个AP的MDK3 **身份验证DoS**
* 捕获**WPA握手**或收集**IVs**以破解WEP网络
* **Reaver WPS**破解（使用NetHunter chroot和外部适配器的小精灵灰尘攻击）

### 其他
* 让应用程序在后台运行，可以选择发出通知
* 将命令或MAC地址复制到剪贴板
* 包括所需的工具，无需手动安装
* 包括Nexmon驱动程序，BCM4339和BCM4358设备所需的库和管理实用程序
* 设置命令以自动启用和禁用监视模式
* 带有自定义字典的**.cap破解文件**
* 创建**自定义操作**并轻松地在访问点或客户端上运行它们
* 使用许多参数对接入点和站点进行排序和过滤
* 将所有收集的信息导出到文件中
* 为设备添加持久性别名（通过MAC），以便于识别 

<img src="https://github.com/chrisk44/Hijacker/raw/master/screenshots/airodump_view.png" width="256" hspace="2"><img src="https://github.com/chrisk44/Hijacker/raw/master/screenshots/mdk_view.png" width="256" hspace="2"><img src="https://github.com/chrisk44/Hijacker/raw/master/screenshots/reaver_view.png" width="256" hspace="2">

[更多截屏](https://github.com/chrisk44/Hijacker/tree/master/screenshots)

## 安装
确保：
* 您使用的是Android 5+
* 您已获取root权限
* 您的固件在无线接口上支持显示器模式

#### 在[这里](https://github.com/chrisk44/Hijacker/releases)获取最新版本。

首次运行Hijacker时，系统将询问您是否要安装nexmon固件或进入主屏幕。 如果已安装固件或使用外部适配器，则可以转到主屏幕。 否则，如果您的设备受支持，请单击“安装Nexmon”以安装Nexmon固件。 完成后，您将进入主屏幕，并开始播放airodump。 确保您已启用WiFi，并且它处于监控模式。

##### 注意：在某些设备上，更改`/system`中的文件可能会触发Android安全功能，并且系统分区将在您重新启动后恢复。

## 故障排除

#### 未找到SU二进制文件！

Hijacker需要root访问权限才能运行。它需要一个`su`二进制文件，该文件是具有root特权执行的shell。在启动时，应用程序会运行`which su`命令。如果您收到此消息，则此命令失败。您可能不是root用户，或者您的root用户解决方案未在可访问PATH的目录中提供`su`二进制文件。

#### 无root权限

Hijacker需要root访问权限才能运行。它通过su运行所有命令。调用su后，您设备上的某个应用（用于管理root用户访问权限，例如SuperSU，Superuser）应该会询问您是否要授予对Hijacker的root访问权限。如果访问被拒绝，您会收到此消息。确保Hijacker被授权运行root命令。

#### 无法创建目录'bin/lib'

这意味着该应用无法在系统内自己的目录中创建'bin'或'lib'目录。如果看到此消息，则说明您的操作系统有问题，Hijacker无法对此做任何事情。

#### 该设备不是ARM构架。

该应用程序是为ARM设备设计和测试的。所有包含的二进制文件和库都是针对该体系结构编译的，无法在其他任何版本上使用。如果收到此消息，则必须手动安装它们（[busybox](https://play.google.com/store/apps/details?id=stericson.busybox&hl=el)，aircrack-ng套件，mdk3，reaver，[无线工具](https://hewlettpackard.github.io/wireless-tools/Tools.html)，[libfakeioctl.so](https://github.com/seemoo-lab/nexmon/tree/master/utilities/libfakeioctl)库），然后在工具可预加载所需库的工具上设置“前缀”选项：“LD_PRELOAD=/path/to/libfakeioctl.so”。

#### Hijacker watchdog检测到问题

Hijacker运行后台服务，以确保应该运行的工具和正在运行的工具以及应该停止的工具都已停止。如果其中一项检查失败，您将收到警告。

*某某没有运行*：这可能是由于某个工具意外停止引起的，这可能是参数错误的迹象，该工具预期应用程序的工作方式不同，设备上的其他软件将其杀死，WiFi处于关闭状态或不在监控模式下 ，甚至是损坏的工具（如果您手动编译的话）。

*某某仍在运行*：这可能是由于该应用程序或单独运行该工具的“停止”操作失败（如果您在后台将应用程序保持打开状态，而是自己运行该工具）。失败的“停止”操作可能是由于拒绝root访问或在应用崩溃后启动应用程序而导致运行“停止”操作没有更改（尽管这不应该发生）引起的。
  
#### 无法打开shell以生成错误报告

该应用程序崩溃了，出现了一个新的活动，并且说它无法打开shell来生成错误报告。这就意味着，它无法打开root shell；它执行了su却失败了。没有/拒绝或配置不正确的root访问权限。
Hijacker需要root用户访问权限才能生成错误报告，因为它需要获取设备的日志文件，尝试运行工具以确保其安装正确，读取WiFi固件等。

#### 无法创建报告（外部存储写入访问被拒绝）

字面意思。

### 杂项

在设置中，有一个选项可以测试工具。如果出了问题，可以单击“复制测试命令”，然后选择失败的工具。这会将测试命令复制到剪贴板，您可以在**root** shell中手动运行该命令，然后查看出了什么问题。 如果所有测试均通过，但您仍然有问题，请随时在此处发布解决问题，或使用应用设置中的“发送反馈”选项。

如果应用程序崩溃，则会出现一个新操作，该操作可以通过电子邮件提交错误报告。您可以确切地看到报告包含的内容，它是一个简单的文本文件。这对Hijacker的开发将非常有帮助，但请记住，该应用程序包含*过滤后的*设备日志，其中可能包含MAC地址，SSID，设备详细信息等信息。

请记住，Hijacker只是这些工具的GUI。它运行工具的方式非常简单，如果所有测试都通过并且您处于监视模式，则应该获得所需的结果。还请记住，这些都是“审核”工具。这意味着它们被用来“测试”您的网络的完整性，因此（您应该希望）这些攻击在您的网络上不起作用。但是，如果在终端上键入命令但未通过应用程序进行攻击时起作用，请随时在此处发布以解决此问题。该应用仍在开发中，因此可能会出现错误。

#### 对于不支持的设备或使用过时的版本，请勿报告错误。

## 警告
### 合法的
在未经您许可的网络上使用此应用程序是非法的。您只能在**您的**网络或您被授权使用的网络上使用它。即使在没有主动对他人使用它的情况下，使用在混杂模式下使用网络适配器的软件也可能被视为非法。对于您如何使用此应用程序以及可能造成的任何损失，我不承担任何责任。

### 设备
该应用程序使您可以选择在设备上安装Nexmon固件。即使该应用执行芯片组检查，也会发生错误。该应用程序当前包括仅适用于BCM4339和BCM4358的Nexmon固件。在设备上安装错误的固件可能会损坏它（我的意思是硬件，而不是恢复出厂设置可修复的东西）。对于此软件对您、您的设备、房屋、小猫或其他任何东西造成的任何损害，我概不负责。

#### 考虑一下自己被警告。

## 捐赠

如果您喜欢我的工作，可以给我买啤酒。 :)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VV5TEHL8S6UQ2)
