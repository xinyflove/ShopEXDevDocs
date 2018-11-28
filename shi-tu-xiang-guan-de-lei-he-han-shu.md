# 视图相关的类和函数

**view::make\(\);\(调用html页面并赋值展示\)**

此方法调用的是 app/base/lib/view/factory.php 文件中的 base\_view\_factory 类 的 make\(\) 方法

**$this-&gt;page\(\);\(调用html页面放在指定布局页面里并赋值展示\)**

函数位置:  
pc端:`topc/lib/controller.php`，文件中的 `public function page($view = null, $data = array())`方法  
wap端:`topwap/lib/controller.php`，文件中的 `public function page($view = null, $data = array())`方法

注意1:  
输出html内容会调用`theme/lib/theme.php`中的`fixThemeMedia($code)`函数，把html内容中的含有images的数据进行替换， 例如:`<img src="images/test.jpg" />`替换成域名+themes+主题文件名+images/test.jpg`<img src="域名/themes/主题文件名/images/test.jpg" />`

