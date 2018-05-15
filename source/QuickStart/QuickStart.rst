快速入门
=================================

.. hint::

   摘要

   本文描述如何入门 KIWI ，这一系统实例构建工具。本文适用于 9.15.1 版本。

入手之前
------------------------

确保安装了 KIWI，以及 :doc:`安装 </Installation/Installation>` 中所述的示例项目。

构建首个镜像
------------------------

你的首个镜像将是一个简单的磁盘镜像，它可以在任何完整的虚拟系统中运行，例如 QEMU 。调用如下 KIWI 指令实现构建：

.. code-block:: shell

   $ sudo kiwi-ng --type vmx system build \
    --description kiwi-descriptions/suse/x86_64/suse-leap-42.3-JeOS \
    --target-dir /tmp/myimage


结束后，在 /tmp/myimage 目录下找到后缀为 .raw 的镜像文件。

运行镜像
------------------------

运行镜像，实际上意味着启动操作系统。为了执行该操作，需要将磁盘镜像挂载到虚拟系统，在我们的示例中，使用 QEMU，启动过程如下：

.. code-block:: shell

   $ qemu \
    -boot c
    -drive file=LimeJeOS-Leap-42.3.x86_64-1.42.3.raw,format=raw,if=virtio \
    -m 4096


