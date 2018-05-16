======================================================
KIWI 文档
======================================================

欢迎使用 KIWI 9.15.1 文档 - 用于构建 Linux 系统实例的命令行工具。

.. sidebar:: 链接

   * `GitHub 源代码 <https://github.com/SUSE/kiwi>`__
   * `GitHub 发布 <https://github.com/SUSE/kiwi/releases>`__
   * `RPM 包 <http://download.opensuse.org/repositories/Virtualization:/Appliances:/Builder>`__
   * `构建测试(x86) <https://build.opensuse.org/project/show/Virtualization:Appliances:Images:Testing_x86>`__
   * `构建测试(arm) <https://build.opensuse.org/project/show/Virtualization:Appliances:Images:Testing_arm>`__
   * `构建测试(s390) <https://build.opensuse.org/project/show/Virtualization:Appliances:Images:Testing_s390>`__

**镜像实例？**

一个实例是一个开箱可用的操作系统镜像，包括用于特殊场景下的预配置应用程序。实例由一个镜像文件提供，并且需要在目标系统或者服务中被部署和激活。

对于 KIWI ，镜像由一个目录下的一组可读的文件集指定，也称之为 `镜像描述文件` 。其中至少需要包括一个XML文件，:file:`config.xml` 或者 :file:`.kiwi` 。同时可能还有其他的文件，如脚本或者配置数据。

**联系我们**

* `邮件列表 <https://groups.google.com/forum/#!forum/kiwi-images>`__

   `kiwi-image` 组织是一个开放组织，任何人都可以 `注册 <mailto:kiwi-images+subscribe@googlegroups.com>`__ ，即便你没有 Google账户。

* IRC

   `#opensuse-kiwi` @ irc.freenode.net

.. toctree::
   :maxdepth: 1

   C0_OverView.rst
   C1_Installation.rst
   C2_QuickStart.rst
   C3_BuildingImages.rst


索引
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

