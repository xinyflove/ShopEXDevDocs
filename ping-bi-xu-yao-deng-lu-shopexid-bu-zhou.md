# 屏蔽需要登录shopexID步骤

把文件 app/desktop/controller/passport.php 复制到二开目录 custom\desktop\controller\passport.php

修改文件 custom\desktop\controller\passport.php

把 第24到33行代码注释掉

```text
/*try{
    if ($service = kernel::service('app_pre_auth_use'))
    {
        $pagedata['desktop_login_verify'] = $service->login_verify();
    }
}
catch (Exception $e)
{
    return view::make('desktop/errors/httpConnect.html', ['message' => $e->getMessage()]);
}*/
```

