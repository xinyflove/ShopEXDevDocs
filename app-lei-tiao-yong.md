# app类调用

在开发过程中我们常用到`app::get()`，这样获取app信息,其实这个`app::get()`中的app在`/bootstrap/aliases.php`文件中 重新定义了 `'app' => 'base_static_app'`, `app::get()`就是`base_static_app`类调用了它的`get()`函数。

其他用到相关函数都可以在这个类找到，常用的函数如下:

app::get\('app\_name'\)-&gt;\_\('字符串'\);//返回对应的字符串,没有对应值则返回,原字符串用于不同语言翻译  
app::get\('app\_name'\)-&gt;model\('table\_name'\);//用于操作数据库  
app::get\('app\_name'\)-&gt;rpcCall\('方法名', '参数', '角色'\);//调用api接口

