# 数据表定义

## finder定义

 用dbschema来定义desktop列表

### label定义

定义在 `desktop finder` 中列的名称

```text
return array (
    'columns' => array (
        'app_id' => array (
            'label' => app::get('base')->_('程序目录'),
        ),
    ),
);
```

### width定义

定义在 `desktop finder` 中列的初始宽度

```text
return array (
    'columns' => array (
        'app_id' => array (
            'label' => app::get('base')->_('程序目录'),
            'width => 150,
        ),
    ),
);
```

### in\_list定义

定义在 `desktop finder` 配置列表项中是否可以勾选显示, 默认值为false.

```text
return array (
    'columns' => array (
        'app_id' => array (
            'label' => app::get('base')->_('程序目录'),
            'width => 150,
            'in_list' => true,
        ),
    ),
);
```

### default\_in\_list定义

定义在 `desktop finder` 列表中初始安装的情况下, 对应列是否默认显示在列表中, 默认值为false.

```text
return array (
    'columns' => array (
        'app_id' => array (
            'label' => app::get('base')->_('程序目录'),
            'width => 150,
            'in_list' => true,
            'default_in_list' => true,
        ),
    ),
);
```

**注意：** 要在列表显示此列必须同时含有in\_list和default\_in\_list参数，缺一不可，如果in\_list为false则不显示，default\_in\_list参数没有作用， default\_in\_list为false则不显示，在配置项有选勾选项。

### filterdefault定义

默认在desktop高级筛选\(搜素\), 中是否默认显示, 默认为false. 如果有相关搜索项配置\(filtertype\), 按配置显示

```text
return array (
    'columns' => array (
        'app_id' => array (
            'label' => app::get('base')->_('程序目录'),
            'width' => 150,
            'in_list' => true,
            'default_in_list' => true,
            'filterdefault' => true,
        ),
    ),
);
```

