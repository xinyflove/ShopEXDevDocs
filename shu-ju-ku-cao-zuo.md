# db数据库操作

 具体操作在`Doctrine\DBAL\Connection`类Connection中

**获取数据库操作对象**

 `$db = app::get('base')->database();`

或者

`$db = app::get('当前app名称')->database();`

## 1 根据sql语句操作

### 1.1 查询操作

**1. 获取单条数据,返回关联数组格式**

```text
$sql = "SELECT * FROM table_full_name WHERE id = 1";
$res = $db->fetchAssoc($sql);
```

**2. 获取单条数据,返回集合数组格式**

```text
$sql = "SELECT * FROM table_full_name WHERE id = 1";
$res = $db->fetchArray($sql);
```

**3. 获取单条数据,返回结果的第一行的单个列的值,用于返回计数结果**

```text
$sql = "SELECT COUNT(*) FROM table_full_name WHERE id = 1";
$res = $db->fetchColumn($sql);
```

**4. 获取多条数据**

```text
$sql = "SELECT * FROM table_full_name";
$res = $db->fetchAll($sql);
```

### 1.2 添加、更新、删除

```text
//执行一条SQL语句并返回受影响的行数。
$row = $db->exec($sql);
```

```text
//使用给定的参数执行SQL插入/更新/删除查询，并返回受影响的行数。
//该方法支持PDO绑定类型和DBAL映射类型。
$row = $db->executeUpdate($sql);
```

## 2.查询构建器

 就是调用了`Doctrine\DBAL\Query`中的QueryBuilder类

```text
$db = app::get('base')->database();
$qb = $db->createQueryBuilder();
```

### 2.1 安全：安全防范SQL注入

 调用方法传参，例如:

```text
$res = $qb->select('*')
            ->from('sysstore_store')
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'1'])
            ->execute()->fetch();
```

### 2.2 构建查询

 `\Doctrine\DBAL\Query\QueryBuilder` 支持创建 `SELECT`，`INSERT`，`UPDATE`，和`DELETE` 查询，使用哪种类型的查询取决于您正在使用的方法。

#### **2.2.1 SELECT 查询 ：在你调用select\(\)方法时开始**

```text
$qb->select('id', 'name')
    ->from('users');
    ->execute()
    ->fetch();//或fetchAll();多条
```

#### **2.2.2 INSERT, UPDATE 和 DELETE查询：**

 你可以通过表名 `insert（$tableName）`、`update($tableName）`和`delete($tableName)`：

```text
$res = $qb->insert('sysstore_store')
            ->setValue('store_name', "'aa'")
            ->setValue('store_desc', "'bb'")
            ->execute();

$res = $qb->update('sysstore_store')
            ->set('store_name', "'mozzie'")
            ->set('store_desc', "'caffrey'")
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'4'])
            ->execute();


$res = $qb->delete('sysstore_store')
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'8'])
            ->execute();
```

#### **2.2.3 WHERE 子句**

 `SELECT`、`UPDATE`和`DELETE`查询类型允许使用以下API:where子句

```text
$qb->select('id', 'name')
    ->from('users')
    ->where('email = ?');
```

 调用`where()`覆盖前面的条件子句，你可以防止这样通过表达式结合引入`andWhere()`和 `orWhere()`方法，或者可以使用表达式来生成where子句

#### **2.2.4 表别名**

 from\(\)方法 接受一个可选的第二个参数指定一个表别名。

```text
$qb->select('u.id', 'u.name')
    ->from('users', 'u')
    ->where('u.email = ?');
```

#### **2.2.5 GROUP BY 和 HAVING**

 `SELECT`语句可以指定`GROUP BY`子句和 `HAVING` 子句，使用 `having()`的效果和使用 `where()`一样，有一致的的`andhaving()`和`orhaving()`方法来结合谓词，对于`GROUP BY`，你可以使用`groupBy()`方法,取代之前的表达式或使用`addGroupBy()`来添加:

```text
$qb->select('DATE(last_login) as date', 'COUNT(id) AS users')
    ->from('users')
    ->groupBy('DATE(last_login)')
    ->having('users > 10');
```

#### **2.2.6 加入条件**

对于`SELECT`子句可以产生不同类型的连接:`INNER`, `LEFT` and `RIGHT`，正确的连接是不跨所有平台移植\(例如Sqlite不支持\)。

联接总是属于from子句的一部分。这就是为什么你必须指定别名的联接部分属于作为第一个参数。第二个和第三个参数你可以指定名称和连接表的别名,第四个参数包含在ON条款。

```text
$qb->select('u.id', 'u.name', 'p.number')
    ->from('users', 'u')
    ->innerJoin('u', 'phonenumbers', 'p', 'u.id = p.user_id');
```

 `join()`方法的用法说明，`innerJoin()`,`leftJoin()`和`rightJoin()`是相同的，`join()`是一个`innerjoin()`速记语法。

```text
$res = $qb->select($row)
		  ->from('sysitem_item', 'SI')
		  ->leftJoin('SI', 'sysitem_item_count', 'SIC', 'SI.item_id=SIC.item_id')
		  ->leftJoin('SIC', 'sysitem_item_status', 'SIS', 'SIC.item_id=SIS.item_id')
		  ->leftJoin('SIS', 'sysitem_item_store', 'SISS', 'SIS.item_id=SISS.item_id')
		  ->where($where)
		  ->setFirstResult( $offset )
		  ->setMaxResults($limit)
		  ->orderBy($orderBy['by'], $orderBy['sort'])->execute()->fetchAll();//或者 fetch()
```

#### **2.2.7 Order-By**

 `orderBy($sort, $order = null)`方法添加`order BY`子句的表达。注意：可选`$order`参数是不安全的用户输入和接受SQL表达式。

```text
$qb->select('id', 'name')
    ->from('users')
    ->orderBy('username', 'ASC')
    ->addOrderBy('last_login', 'ASC NULLS FIRST');
```

 使用`addOrderBy`方法添加,而不是取代`orderBy`条款。

#### **2.2.8 限制条款**

 只有几个数据库厂商的限制条款从MySQL已知,但我们支持此功能对所有供应商使用工作区。使用这个功能,你必须调用方法`setFirstResult($offset)`设置偏移量和`setMaxResults($limit)`设置限制返回的结果。

```text
$qb->select('id', 'name')
    ->from('users')
    ->setFirstResult(10)
    ->setMaxResults(20);
```

#### **2.2.9 VALUES**

 `INSERT`条款设置列的值而插入的值可以用`values()`方法查询构建器:

```text
$qb->insert('users')
    ->values(
        array(
            'name' => '?',
            'password' => '?'
        )
    )
    ->createPositionalParameter(0, $username)
    ->createPositionalParameter(1, $password);
```

 每个后续的调用 `values()`覆盖任何先前的设置值。设置单个值,而不是一次设置全部用`setValue()`方法也是可能的:

```text
$qb->insert('users')
    ->setValue('name', '?')
    ->setValue('password', '?')
    ->createPositionalParameter(0, $username)
    ->createPositionalParameter(1, $password);

// INSERT INTO users (name, password) VALUES (?, ?)
```

 当然你也可以使用这两种方法结合在一起:

```text
$qb->insert('users')
    ->values(
        array(
            'name' => '?'
        )
    )
    ->createPositionalParameter(0, $username);

// INSERT INTO users (name) VALUES (?)

if ($password) {
    $qb->setValue('password', '?')
        ->createPositionalParameter(1, $password) ;

    // INSERT INTO users (name, password) VALUES (?, ?)
}
```

 没有设置任何值，将导致空插入语句：

```text
$qb->insert('users');

// INSERT INTO users () VALUES ()
```

#### **2.2.10 设置条款**

 为更新的条款列设置为新值是必要的,可以用一组`set()`方法查询生成器。请注意,第二个参数允许用户输入的表达式，它是不安全的用户输入:

```text
$qb->update('users', 'u')
    ->set('u.logins', 'u.logins + 1')
    ->set('u.last_login', '?')
    ->createPositionalParameter(0, $userInputLastLogin);
```

#### **2.2.11 构建表达式**

对于更复杂的`WHERE`, `HAVING`或其他条款可以使用表达式构建这些查询部分。您可以借助表达式API，通过调用`$qb -> expr()`,然后调用辅助方法。

最值得注意的是您可以使用表达式来建立嵌套 `And-/Or`语句:

```text
$qb->select('id', 'name')
    ->from('users')
    ->where(
            $qb->expr()->andX(
            $qb->expr()->eq('username', '?'),
            $qb->expr()->eq('email', '?')
        )
    );
```

`andX()`和`orX()`方法接受一个任意数量的参数,可以相互嵌套。

这有一些方法来创建的比较和其他SQL表达式对象上的片段,你可以在API文档上看到。

#### **2.2.12 绑定参数占位符**

 通常在构建一个查询的时候没有必要知道的确切占位符的名字。您可以使用两个助手方法来将一个值绑定到一个占位符和直接使用查询的返回值的占位符:

```text
$qb->select('id', 'name')
    ->from('users')
    ->where('email = ' .  $qb->createNamedParameter($userInputEmail));

// SELECT id, name FROM users WHERE email = :dcValue1

$qb->select('id', 'name')
    ->from('users')
    ->where('email = ' . $qb->createPositionalParameter($userInputEmail));

// SELECT id, name FROM users WHERE email = ?
```

## 3. 事务操作

```text
$db = app::get('sysshop')->database();
$db->beginTransaction();//开启事务
$db->commit();//提交
$db->rollback();//回滚
```

 例子:

```text
$db = app::get('sysshop')->database();
$db->beginTransaction();
try
{
    $result = $this->objMdlEnterapply->save($postdata);
    if(!$result)
    {
	throw new \LogicException('申请提交失败');
    }
    $db->commit();
    return true;
}
catch(\LogicException $e)
{
    $db->rollback();
    throw new \LogicException($e->getMessage());
    return false;
}
```

