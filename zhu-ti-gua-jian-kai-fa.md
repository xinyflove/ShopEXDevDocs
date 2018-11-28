# 主题挂件开发

## 1. 主题挂件文件目录

主题挂件放在主题目录下的widgets文件夹下，例如我开发的blueberrymall主题  
public/themes/blueberrymall/widgets

## 2. 挂件文件

例如我们开发一个 Logo挂件\(logo\)，首先在widgets目录下创建logo文件夹  
public/themes/blueberrymall/widgets/logo/ 里面含有如下文件：

`widgets/logo/images/icon.jpg` 可选，挂件图标  
`widgets/logo/_config.html` 必选，挂件配置文件  
`widgets/logo/default.html` 必选，挂件展示模版文件  
`widgets/logo/theme_widget_logo.php` 必选，挂件展示数据处理文件\(注意:挂件展示数据处理文件由theme\_widget\_ 链接 挂件名\(logo\)组成\)  
`widgets/logo/widgets.php` 必选，挂件描述文件

### 2.1 widgets.php文件

挂件描述信息文件，内容如下：

```text
/*基础配置项*/
$setting['author'] = 'www.tvplaza.cn';//作者信息
$setting['name'] = '底部二维码';//挂件名称
$setting['version'] = 'v1.0';//版本信息
$setting['order'] = 0;//排序
$setting['stime'] = '2018-7';//创建时间
$setting['catalog'] = '辅助相关';//分类
$setting['usual'] = '0';//是否常用，1常用|0不常用
$setting['description'] = '用于底部展示二维码信息';//描述
$setting['userinfo'] = '';//用户信息
$setting['template'] = array(//模版
                            'default.html'=>app::get('b2c')->_('默认')
                        );

/*首次默认配置项*/
/*给变量$setting配置默认数据*/
```

### 2.2 \_config.html文件

挂件编辑文件，用于配置数据

### 2.3 theme\_widget\_logo.php文件

挂件前端展示数据处理文件，用于处理配置数据

```text
//1.函数名即为文件名
//2.$setting配置的数据
//3.如果传参$setting加上'&'(&$setting)，则在函数中可修改输出$setting变量数据
//4.返回的数据在default.html文件中，可用任意变量接收
function theme_widget_footer_qrcode($setting) {
    $datas = array();
    
    //处理数据code
    
    return $datas;
}
```

### 2.4 default.html文件

挂件模版文件，用于渲染数据

挂件展示由theme\_widget\_logo.php处理数据，theme\_widget\_logo.php 中的theme\_widget\_logo\($setting\)方法  
返回数据，并在default.html渲染数据，原则上default.html中可以由任意的变量来接收theme\_widget\_logo.php文件  
返回的数据，变量$setting接收 为了防止变量冲突和规范性，变量$datas来接收theme\_widget\_logo.php文件处理后返回的数据。

