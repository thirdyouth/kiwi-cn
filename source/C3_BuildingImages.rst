-----------------------------------------
构建镜像
-----------------------------------------

.. hint::

   本文概述了KIWI支持的镜像类型。在开始KIWI构建镜像之前，了解不同的镜像类型及含义非常重要。


.. toctree::
   :maxdepth: 1

   building/build_live_iso
   building/build_vmx_disk
   building/build_oem_disk
   building/build_pxe_root_filesystem
   building/build_docker_container
   building/build_containerized
   building/build_in_buildservice
   building/working_with_images


* ISO 混合 Live 镜像

* 虚拟磁盘镜像

* OEM 可扩展磁盘镜像

* PXE 根文件系统镜像

* Docker 容器镜像

支持发行版
================================

KIWI 可以构建为不同的发行版构建上述镜像类型，包括或者高于一下版本列表：

* CentOS 7
* Fedora 25
* openSUSE Leap 42
* Red Hat Enterprise 7
* SUSE Linux Enterprise 12
* Tumbleweed
* Ubuntu Xenial

对于其他旧的发行版，可以考虑使用以前的 KIWI 版本 v7.x,更多信息有关早期 kiwi，可以参考 `早期 KIWI 与 新一代对比`_
