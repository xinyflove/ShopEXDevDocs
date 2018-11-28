# 创建一个对象

```text
kernel::single($class_name,$arg=null)


//例如:

kernel::single('sysbankmember_bank')
//生成的是目录为sysbankmember/lib/bank.php 里的class为sysbankmember_bank的对象

kernel::single('sysbankmember_data_bank')
//生成的是目录为sysbankmember/lib/data/bank.php 里的class为sysbankmember_data_bank的对象
```

