# 定时任务

## 配置定时任务

运行商派的环境一般是Linux系统，所以不用考虑如何在Windows上配置，

```text
#检查 /home/目录下是否有www目录，没有则创建一个
mkdir /home/www
#配置定时任务，必须配置的是www权限的crontab，不要在root或者其他用户下配置
crontab -uwww -e
#将下面的配置复制进去
* * * * *  /data/httpd/script/queue/queue.sh /usr/local/php56/bin/php > /dev/null
* * * * *  /usr/local/php56/bin/php  /data/httpd/script/crontab/crontab.php >/dev/null
```

说明:  
`/data/httpd/`是系统根目录  
`/usr/local/php56/bin/php/`php运行目录

## 创建一个定时任务

最近在做个`app`名为`foodmap`的应用，就以这个应用为例，在`foodmap/`目录下创建`crontab.xml`文件

写入以下代码:

```text
<cronentries>
    <cron id="foodmap_tasks_supplierSync">
        <description>批量跟接口同步供货商信息</description>
        <schedule>* * * * *</schedule>
        <enabled>true</enabled>
    </cron>
</cronentries>
```

说明:  
`<cron id="foodmap_tasks_supplierSync">`会去调用`foodmap/lib/tasks/supplierSync.php`文件中的`foodmap_tasks_supplierSync`类  
`<description>批量跟接口同步供货商信息</description>`定时任务描述  
`<schedule>* * * * *</schedule>`定时任务运行周期，跟linux配置定时任务规则相同，此规则为一分钟调用一次  
`<enabled>true</enabled>`是否启用

创建`foodmap/lib/tasks/supplierSync.php`文件，写入一下代码:

```text
class foodmap_tasks_supplierSync extends base_task_abstract implements base_interface_task{
    
    function exec($params = null)
    {
        // TODO: Implement exec() method.
        logger::info('执行任务开始！');
        //要执行定时任务的代码
        logger::info('执行任务结束！');
    }
}
```

说明:  
类`foodmap_tasks_supplierSync`继承`base_task_abstract`实现`base_interface_task`后，必须实现`exec()`方法，这个方法就是默认执行任务的函数。

提示:  
所有的定时任务先放到队列中，然后在被执行。  
在总后台打开 系统&gt;定时任务 来查看创建的定时任务信息。

