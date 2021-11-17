新需求，需要对2位小数的浮点数处理，发现intval出现精度丢失的问题，intval(16.65 * 100) = 1664 搜索了一波，发现是个人问题，没关注到这里。标记一下
https://www.laruence.com/2013/03/26/2884.html
*  解决方案
  * https://www.php.net/manual/zh/function.bcmul
  * https://www.php.net/manual/zh/function.intval.php
    ```php 
      <?php
        $n="19.99";
        print intval($n*100); // prints 1998
        print intval(strval($n*100)); // prints 1999
        ?>
        
    ```
