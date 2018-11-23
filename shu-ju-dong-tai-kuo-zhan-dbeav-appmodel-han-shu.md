# 数据动态扩展\(dbeav app\)model函数

 原始app目录文件 `app/dbeav/lib/model.php`

## 获取app的model

```text
app::get('sysactivityvote')->model('active');//获取app为sysactivityvote的表active的model
```

即使没有对应的active的model文件只要继承了base\_db\_model都会提供基础的数据库操作函数

active的model文件在`/sysactivityvote/model/active.php`

## 列表操作符查询

 例如:`app::get('sysuser')->model('account')->getList('user_id',$tmpfilter);`

|  操作符     |  代码     |  代表SQL语句 |
| :--- | :--- | :--- |
|  IN |  `$tmpfilter['user_id|in']=array(1,2,3,4,.....)` |  user\_id IN \(1,2,3,4,...\) |
|  NOT IN |  `$tmpfilter['user_id|notin']=array(1,2,3,4,.....)` |  user\_id NOT IN \(1,2,3,4,...\) |
|  LIKE |  `$tmpfilter['user_name|has']='小明'` |  user\_name LIKE '%小明%' |
|  LIKE |  `$tmpfilter['user_name|head']='小明'` |  user\_name LIKE '小明%' |
|  LIKE |  `$tmpfilter['user_name|foot']='小明'` |  user\_name LIKE '%小明' |
|  NOT LIKE |  `$tmpfilter['user_name|nohas']='小明'` |  user\_name NOT LIKE '%小明%' |
|  &gt; |  `$tmpfilter['user_age|than']='18'` |  user\_age &gt; '18' |
|  &lt; |  `$tmpfilter['user_age|lthan']='18'` |  user\_age &lt; '18' |
|  =  | `$tmpfilter['user_age|nequal']='18'`或 `$tmpfilter['user_age|tequal']='18'` 或 `$tmpfilter['user_age']='18'` |  user\_age = '18'   |
|  &lt;&gt; |  `$tmpfilter['user_age|noequal']='18'` |  user\_age &lt;&gt; '18' |
|  &gt;= |  `$tmpfilter['user_age|bthan']='18'` |  user\_age &gt;= '18' |
|  &lt;=  |  `$tmpfilter['user_age|sthan']='18'` |  user\_age &lt;= '18' |
|  BETWEEN  |  `$tmpfilter['user_age|between']=array(18,20)` |  user\_age BETWEEN 18 AND 20 \(未验证\) |

## batch\_dump\(\) _关联查询_ 函数

要提前设置model里的关联设置  
参考文档:[http://club.ec-os.net/doc/ecos/framework-ecos/advance/dbeav/dbeav.html\#id19](http://club.ec-os.net/doc/ecos/framework-ecos/advance/dbeav/dbeav.html#id19)

