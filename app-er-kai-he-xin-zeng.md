# 应用（app）二开和新增

## 应用（app）二开

**不建议**在 `app/` 目录，原有的app进行二次开发，默认二次开发目录为 `custom/`，不用把需要二次开发的原有app目录整个复制到custom目录下，只把需要修改的文件复制到对应位置进行修改开发。

**例如:**我们要修改`app/sysitem/controller/admin/item.php`文件,把此文件复制到`custom/sysitem/controller/admin/item.php`进行修改 开发。

如果我们想要修改默认二次开发目录，在文件 `config/compatible.php` 把 `define('CUSTOM_CORE_DIR', ROOT_DIR.'/custom');` 中的 `custom` 修改你想要定义的目录名称，然后在此目录下进行二次开发。

## 新增应用（app）

 以app名称为notebook为例，在 `app/` 目录下创建 `app/notebook/` 目录,然后创建 `app/notebook/app.xml`文件,文件内容为:

```text
<app>
    <name>Test App</name><!--填写应用名称-->
    <description>Test App应用描述</description><!--填写描述-->
    <type>service</type><!--app类型-->
    <author><!--填写作者信息-->
        <name>Caffrey Xin</name><!--填写作者名称-->
        <email>xinyflove@sina.com</email><!--填写作者邮箱-->
        <url>xinyufeng.net</url><!--填写作者链接地址-->
    </author>
    <version>0.1</version><!--版本号-->
    <license>不需要证书</license><!--证书信息-->
    <depends><!--填写依赖包信息-->
        <app>desktop</app><!--填写具体依赖的app目录名称-->
    </depends>
</app>
```

{% hint style="danger" %}
注意:如果涉及到数据库表的使用`type`标签内容一定要为`service`,并且要在 `app/` 目录下创建 `app/dbschema/` 目录.
{% endhint %}

然后在 `custom/` 目录下创建 `custom/notebook/` 目录,把 `app/notebook/app.xml` 文件,复制到 `custom/notebook/app.xml` 文件.

## app目录说明

|  路径 |  说明 |
| :--- | :--- |
|  app/notebook/model |  模型目录 |
|  app/notebook/view |  视图目录 |
|  app/notebook/controller |  控制器目录 |
|  app/notebook/dbschema |  数据库表结构定义 |
|  app/notebook/lang |  语言包文件夹 |
|  app/notebook/lib |  php类库文件 |

