#Mongodb for ThinkPHP 驱动备忘录

## 支持在条件数据中使用`_where`字段来指定查询Mongodb的整个条件，此条件ThinkPHP会原封不动的传给MongoDB PHPLIB
例如：
``` 
D('Article')->field('sort_id,title,pic_size3')->where(array('_where'=>array (
  '$and' => array (
    array ('id' => 97456),
    array (
      '$or' => array (
        array ('status' => 1),
        array ('status' => 3),
      ),
    ),
  ),
)))->find(); 
```

## 支持在options中指定`options`字段值来设置作用于MongoDB的选项
例如：
```
D('Article')->where(array('status'=>1))->select(array(
    'options'=>array(
        'skip'=>10,
        'limit'=>10,
        'projection'=>array('_id'=>0) //是否(1/0)返回`_id`字段,此处为不返回
    )
)); 
```
支持的选项：http://php.net/manual/en/mongodb-driver-query.construct.php


## 支持在`field`方法中用数组方式指定返回字段
例如：
```
D('Article')->field(array('_id'=>0))->where(array('status'=>1))->limit(0,10)->select(); 
```