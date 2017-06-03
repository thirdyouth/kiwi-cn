Readme
===============================

该仓库是 opensuse文档说明的静态 html 文档生成库，主要包含 openSUSE 系统使用方面的文档翻译，及其他开源工具的使用文档翻译和整理。

构建依赖
-------------------------------

* sphinx
* make
* sphinx_py3doc_enhanced_theme

构建方法
--------------------------------

.. code-block:: shell

   make html
   
在上述命令完成之后，将会在 build/html 中生成所有的静态页面。

构建清理
--------------------------------

.. code-block:: shell

   make clean
   

