
## 现象描述
设置数据库大小写不敏感失败，报错如下：
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)

## 可能原因
- 存在大写的库表名。
- 数据库版本为8.0。

## 处理步骤
### 存在大写的库表名
核实该实例下的库、表是否都是小写，如有大写的库表名，需要全部改为小写，然后修改 lower_case_table_names 参数。
>!修改 lower_case_table_names 参数会造成数据库重启。
>
- 排查是否有大写的表
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- 排查是否有大写的库
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

### 数据库版本为8.0
若数据库版本为8.0，则无法修改 lower_case_table_names 参数，8.0版本默认区分大小写。
