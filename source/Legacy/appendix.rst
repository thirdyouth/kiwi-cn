############################################
附录：KIWI 操作手册页
############################################

本节内容将会提供 KIWI 的 man 手册页，以及 :file:`config.sh` 和 :file:`index.sh` 中可以使用的函数。


*************************************************************
kiwi
*************************************************************

kiwi — 用于创建操作系统镜像

kiwi 概要
=============================================================

.. code-block:: shell

   kiwi { -l | --list }

.. code-block:: shell

   kiwi { -o | --clone } image-path { -d } destination

.. code-block:: shell

   kiwi { -b | --build } image-path { -d } destination

kiwi 基础
=============================================================


kiwi 常用参数
=============================================================


kiwi 镜像准备和创建
=============================================================

* 镜像准备：

  .. code-block:: shell

     kiwi { -p | --prepare } image-path 
     { -r | --root } image-root [--cache directory]

* 镜像创建：

  .. code-block:: shell

     kiwi { -c | --create } image-root 
     { -d | --destdir } destination [--type image-type]

kiwi 镜像升级
=============================================================

.. code-block:: shell

   kiwi { -u | --upgrade } image-root [--add-package name] [--add-pattern name]


kiwi 系统分析
=============================================================

.. code-block:: shell
  
   kiwi { --describe } name

kiwi 镜像后处理模式
=============================================================

镜像后处理模式用于特殊镜像部署任务，如镜像安装到 U 盘。因此可以将这一步成为准备和创建之后的第三步。KIWI 根据指定的输出镜像类型和属性自动调用后处理模块，但是也可以通过手动调用处理。

.. code-block:: shell

   kiwi --bootvm initrd --bootvm-system systemImage [--bootvm-disksize size]

.. code-block:: shell

   kiwi --bootcd initrd

.. code-block:: shell

   kiwi --bootusb initrd

.. code-block:: shell

   kiwi --installcd initrd --installcd-system raw-system-image

.. code-block:: shell

   kiwi --installstick initrd --installstick-system raw-system-image

.. code-block:: shell

   kiwi --installpxe initrd --installpxe-system raw-system-image
   
kiwi 镜像格式转换
=============================================================

KIWI 格式转换对于其他镜像格式的创建非常有用，例如,用于 VMware 的 vmdk，或者开放虚拟机格式 ovf。在进行转换时，如果在 XML 描述中存在机器部分说明，KIWI 也会根据不同格式，创建相应的虚拟机配置。

.. code-block:: shell

   kiwi --convert systemImage [--format vmdk|ovf|qcow2|vhd]

kiwi 辅助工具
=============================================================


kiwi 全局参数
=============================================================



kiwi 镜像准备参数
=============================================================

kiwi 镜像升级/准备参数
=============================================================

kiwi 镜像创建参数
=============================================================

kiwi 更多信息
=============================================================

有关 KIWI 更多信息，可以参考如下文件：

* http://en.opensuse.org/Portal:KIWI ， KIWI维基页面。

* :file:`config.xml` ，XML 配置文件，包含了镜像创建的各个方面。

* :file:`file:///usr/share/doc/packages/kiwi/kiwi.pdf` ，系统文档，描述了镜像类型支持的详细信息。

* :file:`file:///usr/share/doc/packages/kiwi/schema/kiwi.xsd.html` ，KIWI RELAX NG XML 格式规范文档。

*************************************************************
kiwi::config.sh
*************************************************************

KIWI::config.sh — KIWI 镜像描述定制文件

config.sh 描述
=============================================================

KIWI 镜像描述允许使用可选的 :file:`config.sh` bash 脚本。该脚本可用于从给定的未打包镜像创建的所有镜像进行合理的改动（因为 config.sh 在创建步骤开始之前运行）。基本上，该脚本设计用于添加镜像的操作系统配置。这里的配置是指，操作系统安装过程中仅执行一次的所有任务，如激活服务程序，创建配置文件，准备首次启动工作流程环境，等等。:file:`config.sh` 脚本在下述 kiwi 内置配置任务之后调用：用户/用户组，复制重载根目录，和 autoyast 设置，如果 :file:`config.sh` 以非 0 代码退出，kiwi 进程也将会失败退出。

示例 A.1. config.sh 模板
-------------------------------------------------------------

::

  #======================================
  # Functions...
  #--------------------------------------
  test -f /.kconfig && . /.kconfig
  test -f /.profile && . /.profile

  #======================================
  # Greeting...
  #--------------------------------------
  echo "Configure image: [$kiwi_iname]..."

  #======================================
  # Mount system filesystems
  #--------------------------------------
  baseMount

  #======================================
  # Call configuration code/functions
  #--------------------------------------

  #======================================
  # Umount kernel filesystems
  #--------------------------------------
  baseCleanMount

  #======================================
  # Exit safely
  #--------------------------------------
  exit 0

config.sh 常用功能
=============================================================

:file:`.kconfig` 文件允许使用常见函数集。SUSE 独有的功能函数前缀为 *suse* 。对所有 Linux 系统适用的功能函数前缀为 *base* 。下属列表描述了 :file:`config.sh` 脚本内可用的功能函数。

* [baseCleanMount]
  
  卸载系统文件系统 :file:`/proc` ，:file:`/dev/pts` ，和 :file:`/sys` 。
  
* [baseDisableCtrlAltDel]

  在 :file:`/etc/inittab` 文件中禁用 :kbd:`Ctrl-Alt-Del` 组合按键。
  
* [baseGetPackagesForDeletion]

  返回将被删除的包名称。
  
* [baseGetProfilesUsed]

  返回用于构建镜像的配置文件名称。
  
* [baseSetRunlevel {value}]

  设置默认运行级别。

* [baseSetupBoot]

  设置 :file:`linuxrc` 作为 init 初始化程序。
  
* [baseSetupBusyBox {-f}]

  激活 busybox，如果从 :file:`busybox/busybox.links` 文件安装所有符号链接，您使用 :option:`-f` 参数强制选择指定程序进入 busybox ，例如：
  
  .. code-block:: shell
  
     baseSetupBusyBox -f /bin/zcat /bin/vi
     
* [baseSetupInPlaceGITRepository]

  为根目录创建相应的 git 仓库。该过程需要一些时间，并且可能遇到一些二进制数据处理有关和的问题。
  
* [baseSetupInPlaceSVNRepository {path_list}]

  为指定目录创建相应的 svn 仓库。标准的调用方式如下：
  
  .. code-block:: shell
  
     baseSetupInPlaceSVNRepository /etc /srv /var/log

* [baseSetupPlainTextGITRepository]


  创建根目录的 git 仓库，只包含所有的普通文本文件。
  
* [baseSetupUserPermissions]

  查询 :file:`/etc/passwd` 中列出的所有用户的 home 目录，并修改其中所有文件的属主为相应的用户和用户组。
  
* [baseStripAndKeep {list of info-files to keep}]

  strip* 相关功能函数的辅助函数，读取文件的 stdin 行，检查需要删除的参数：那些文件需要保留。
  
* [baseStripDocs {list of docu names to keep}]

  删除参数内指定保留文档之外的所有其他文档。
  
* [baseStripInfos {list of info-files to keep}]

  删除参数内指定 info 文件之外的其他 info 文件。
  
* [baseStripLocales {list of locales}]  

  删除参数内指定的本地化配置之外的其他本地化配置。
  
* [baseStripMans {list of manpages to keep}]

  删除参数内指定的程序手册页之外的其他程序手册页，例如： baseStripMans more less
  
* [baseStripRPM]

  删除 :file:`config.xml` 配置文件中 type=delete 部分中定义的 rpm 包。
  
  
* [suseRemovePackagesMarkedForDeletion]


* [baseStripTools {list of toolpath} {list of tools}]

* [baseStripUnusedLibs]

* [baseUpdateSysConfig {filename} {variable} {value}]

* [Debug {message}]

* [Echo {echo commandline}]

* [Rm {list of files}]

* [Rpm {rpm commandline}]
* [suseConfig]
* [suseInsertService {servicename}]
* [suseRemoveService {servicename}]
* [baseInsertService {servicename}]
* [baseRemoveService {servicename}]
* [baseService {servicename} {on|off}]
* [suseActivateDefaultServices]
* [suseSetupProduct]
* [suseSetupProductInformation]
* [suseStripPackager {-a}]

config.sh 配置环境变量
=============================================================

:file:`.profile` 环境文件包含了下述的环境参数设置，上述的一些功能函数将会用到这些变量。

* [$kiwi_compressed]

  该变量所赋的值是 :file:`config.xml` 文件中 **type** 元素中的压缩属性。

* [$kiwi_delete]

  该变量中的所有包是 :file:`config.xml` 文件中 **type="delete"** 部分所指定包的部分列表。

* [$kiwi_drivers]

  该变量定义一个以逗号分割的驱动程序列表，用于 :file:`config.xml` 文件中 **drivers** 部分。

* [$kiwi_iname]

  该变量定义 :file:`config.xml` 所列出的镜像名称。

* [$kiwi_iversion]

  该变量定义镜像版本字符串，如 major.minor.release 

* [$kiwi_keytable]

  The contents of the keytable setup as done in config.xml

* [$kiwi_language]

  The contents of the locale setup as done in config.xml

* [$kiwi_profiles]

  A list of profiles used to build this image

* [$kiwi_size]

  The predefined size value for this image. This is not the computed size but only the optional size value of the preferences section in config.xml

* [$kiwi_timezone]

  The contents of the timezone setup as done in config.xml

* [$kiwi_type]

  The basic image type. Can be a simply filesystem image type of ext2, ext3, reiserfs, squashfs, cpio, or one of the following complex image types: iso, split, usb, vmx, oem, xen, or pxe.

*************************************************************
kiwi::images.sh
*************************************************************


images.sh 描述
=============================================================

*************************************************************
kiwi::kiwirc
*************************************************************
