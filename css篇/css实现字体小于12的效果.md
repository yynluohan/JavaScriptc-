# css实现字体小于12的效果

  一般设置font-size小于12的时候，显示都是12，无法实现更小的字体了。但是面对有些UI设计图出现小于10px的字体，可以用这么实现：

  ## 移动端
  ```
  .font {
    // 10 / 12 = 0.83
    transform: scale(0.83);
  }
  ```

  ## pc端
  避免不支持 CSS3 浏览器的情况，我们也可以通过降级处理，将字体变回12px；最后兼容 IE：*font-size:10px;

  ```
  .font{
    font-size: 12px;
    transform: scale(0.83,0.83) ;
    *font-size: 10px;
  }
  ```
