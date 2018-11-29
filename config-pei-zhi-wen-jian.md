# config配置文件

 配置文件放在`/config/`目录下，生产环境配置文件在`/config/production`/目录下。

## 获取与配置设置

例子:

```text
config::get('storepermission.common.nologin'));
```

获取的是:

`/config/production/storepermission.php`文件的 数组中 `['common']`的`['nologin']`中的数组值。

```text
return array(

    'common' => [
        'permission' =>[  //公共权限的路由
			    'topstore.signin',
			    'topstore.simpleSignin',
			    'topstore.postsignin',
			    'topstore.nopermission',
			    'topstore.postnosignin',
        ],
        'nologin' => [	//不需要登录的路由
			    'topstore.signin',
			    'topstore.simpleSignin',
			    'topstore.postsignin',
			    'topstore.nopermission',
			    'topstore.postnosignin',
         ]
    ],
    
);
```

## 配置文件作用

### apis.php

定义api接口路由文件

### app.php

参数：

'debug' =&gt; true,    开启调试模式



