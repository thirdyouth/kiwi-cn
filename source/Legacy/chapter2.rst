*************************************************************
第二章：安装
*************************************************************

安装 KIWI 包
===============================

KIWI 随所有的 SUSE 发行版发布，但是并未默认安装。对于 SUSE Linux Enterprise 11，KIWI 包含在软件开发套件(SDK)，而不是主安装媒介。最小化的 KIWI 安装需要安装 kiwi 包，以及至少以下一种包含各种镜像类型启动描述的软件包：

* kiwi-desc-isoboot：Live ISO 启动模板
* kiwi-desc-netboot：PXE 网络启动模板
* kiwi-desc-oemboot：可扩展虚拟机启动模板
* kiwi-desc-vmxboot：虚拟机启动模板

同时建议安装 kiwi-doc 包，其中包含了文档资料。对于完整的 KIWI 包，可以通过 :command:`zypper se kiwi` 指令查看。 


安装最新可用版本
-------------------------------

KIWI 是一个活跃项目，并且经常会发布新的版本。所有 SUSE 发行版都可用的最新 KIWI 版本包都可以通过 Virtualization:Appliances 库进行获取 http://download.opensuse.org/repositories/Virtualization:/Appliances/ 。

从源码安装运行
===============================

KIWI 通过 Github 中的一个 git 仓库进行开发和管理。您可以通过下面的指令获取最新源代码：

.. code-block:: shell

   git clone https://github.com/openSUSE/kiwi.git
   
在从源码开始运行之前，您需要确保满足所有的依赖条件。从检出目录(:file:`kiwi/`)中通过如下指令获取所需软件包列表：

.. code-block:: shell

   awk '/BuildRequires:/ { print $2 | "sort" }' rpm/kiwi.spec

在安装完所有的依赖之后，从检出目录中运行测试集：

.. code-block:: shell

   make test

如果所有测试通过，所有依赖项满足，然后可以从检出目录中执行 KIWI，指令如下：

.. code-block:: shell

   ./kiwi
   

为了检出最新可用版本，直接在 KIWI 检出目录中执行 :command:`git pull` 命令。 
   

