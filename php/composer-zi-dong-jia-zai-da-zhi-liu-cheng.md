---
description: 'composer也算接触很久,认真的看下它的自动加载，并记录一波'
---

# composer 自动加载大致流程



* 执行composer 命令后，在当前目录下会生成一个vendor目录，在vendor目录中有一个composer目录
  * ClassLoader.php                
  * autoload\_classmap.php    
  * autoload\_files.php
  * autoload\_namespaces.php    
  * autoload\_psr4.php    
  * autoload\_real.php    
  * autoload\_static.php
* composer 支持的自动加载类型
  * psr-4  -&gt;  autoload\_psr4.php    
  * psr-0  -&gt;  autoload\_namespaces.php    
  * class-map -&gt;  autoload\_classmap.php    
  * files   -&gt;  autoload\_files.php
* 根据设置的自动加载类型，会汇总至 autoload\_static.php
* composer 的autoload 文件内是返回 autoload\_real.php
* autoload\_real.php    的getLoader 会设置 ClassLoader ,并注册回调函数。最终通过ClassLoader-&gt;loadClass 实现自动加载

