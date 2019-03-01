# 模型（model）

 通常情况下数据库的一个表会对应一个 **dbschema定义文件\(数据库表定义文件\)** 和一个 model 。

在看代码的时候会有困惑, 有些表找得到**dbschema定义文件**却找不到对应的**model**文件, 但仍然能调用这个本不该存在的model. 这是因为**虚拟model**机制, 当实例化model时如果找不到对应的model类时, 会去找对应的dbschema定义文件,如果找到就会依据dbschema定义文件建立虚拟的model类作为供给。

调用流程图：

![](.gitbook/assets/2019030101%20%281%29.jpg)

### model的命名规则

`{$appid}_mdl{$mod_path}`

例如:

```text
model: b2c_mdl_cart_objects
$app_id = b2c
$mod_path = cart/objects.php
```

### model存放位置

`app/{$app_id}/model/{mod_path}/`

例如:

```text
b2c_mdl_cart_objects
存放位置: app/b2c/model/cart/objects.php
```

