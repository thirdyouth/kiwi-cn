安装
=================================

.. hint::

   本文描述如何安装 KIWI 。除了可以通过推荐的 rpm 安装方式，它也通过 pypi 提供，可以通过指令 pip 进行安装。

KIWI 可以通过不同的方式进行安装。对于本节，仅描述通过包管理器进行的包安装方法。

对于新的 KIWI 版本，软件包在 `openSUSE 构建服务 <http://download.opensuse.org/repositories/Virtualization:/Appliances:/Builder>`_ 上提供。

安装 KIWI ，过程如下：

1. 在浏览器中打开链接 http://download.opensuse.org/repositories/Virtualization:/Appliances:/Builder 。

2. 在你使用的系统中右键点击链接，复制 URL 链接地址。对于 Firefox ，它是菜单 *复制链接地址* 。

3. 在你的命令杭中插入上一步骤拷贝的链接。 DIST 占位符包含了对应的版本，使用 **zypper ar** 将其加入到你的仓库列表：

   .. code-block:: shell

       $ sudo zypper ar -f http://download.opensuse.org/repositories/Virtualization:/Appliances:/Builder/<DIST>

4. 安装 KIWI：

   .. note::

      多个 python 包

      这一版本的 KIWI 同时提供了 python2 和 python3 的版本。下面的信息基于 python3-kiwi 包的安装。

   .. code-block:: shell 

       $ sudo zypper in python3-kiwi


实例描述示例
-----------------------------------------

为了使用下一代的 KIWI ，有一个 GitHub 项目托管了一些实例描述示例。如果需要示例入门，可以下载如下项目：

.. code-block:: shell 

   $ git clone https://github.com/SUSE/kiwi-descriptions 

