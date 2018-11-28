# finder的使用

首先我们了解一下，finder展示在什么地方，如下如↓

![finder&#x5C55;&#x793A;&#x533A;&#x56FE;&#x7247;](.gitbook/assets/finder_area.png)

finder展示区由7分部组成，分别是：

1. finder标题
2. 操作按钮区
3. 快捷搜索
4. 查看列
5. 自定义列
6. 高级筛选
7. 分页区

> 我们平时做任何web应用大概都少不了后台管理功能， 这之中最常看到的大概就是：数据列表，对数据进行单条查看，删除，搜索列表数据。finder就是做这样工作的，要做到这些事情只需简单的给一个方法传几个参数而已

## 调用finder方法

1.控制器继承`desktop_controller`类，`desktop_controller`类封装了`finder()`方法。

2.控制器方法调用`finer()`方法，`$this->finder()`;

例子：

```text
class testapp_ctl_test extends desktop_controller{
	function index()
	{
	   $this->finder(
		   'testapp_mdl_test',
		   array(
			   'title'=>app::get('testapp')->_('finder标题'),
			   'actions'=>array(
				   array(
					   'label'=>app::get('testapp')->_('按钮名称'),
					   'href'=>'?app=testapp&ctl=test&act=add','target'=>'_blank'
				   ),
				   array(
					   'label'=>app::get('testapp')->_('删除'),
					   'icon' => 'download.gif',
					   'submit' => '?app=testapp&ctl=test&act=doDelete',
					   'confirm' => app::get('testapp')->_('确认操作提示文字'),
				   ),
			   ),
			   'use_buildin_set_tag'=>true,//默认false
			   'use_buildin_delete'=>true,//默认true
			   'use_buildin_export'=>true,//默认false
			   'use_buildin_import'=>true,//默认false
			   'use_buildin_tagedit'=>true,
			   'base_filter'=>array( //对列表数据进行过滤筛选
				   'order_refer'=>'local',
				   'disabled'=>'false'
			   ),
			   'top_extra_view'=>array('app名称'=>'html模版页面路径'),
			   'use_view_tab'=>true,
			   'use_buildin_filter' => true,//默认false
			   'use_buildin_refresh' => true,//默认true
			   'use_buildin_setcol' => true,//默认true
			   'use_buildin_selectrow' => true,//默认true
			   'allow_detail_popup' => true,
		   )
	   );
	}
}
```

##  finder方法参数

 1.第一个参数是字符串，（上例中是`testapp_mdl_test`），是model里的class名，它决定了finder列表的数据源，默认情况下是`testapp_mdl_test`类里的`getList`方法返回的数据。

 2.第二个参数是数组，这个数组内涵相当丰富，解释如下：

`title`: 标题\(图中的【1区】显示出来的内容\)

`actions`: 自定义控制项\(图中的【2区】里的内容除了显示内置的操作以外，还可以自定义添加新操作，参照上面格式。\)

以下是内置控制项

`use_buildin_set_tag`: 是否显示设置标签操作\(值ture/false\)

`use_buildin_tagedit`: 是否显示标签管理操作\(值ture/false\)

`use_buildin_delete`: 是否显示删除操作\(值ture/false\)

`use_buildin_export`: 是否显示导出操作\(值ture/false\)

`use_buildin_import`: 是否显示导入操作\(值ture/false\)

`base_filter`： 对列表数据进行过滤筛选，参照上面格式\(值 数组\)

`top_extra_view` 在finder列表头部增加其他自定义html显示,如`top_extra_view=>array('app名称'=>'html模版页面路径');`

`use_view_tab`: 是否显示finder中的tab（如果有），有无需看控制器中是否有`_views`方法。

`use_buildin_filter`: 是否使用高级筛选 图中【6区】

`use_buildin_refresh`: 是否显示刷新操作\(列表配置项旁\)

`use_buildin_setcol`: 是否显示列表配置项

`use_buildin_selectrow`: 是否显示每条记录前的复选按钮

`allow_detail_popup`: 是否显示查看列中的弹出查看图标（图 【4区】第二个图标）



