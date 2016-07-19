####基于SQLite3轻量级封装,一行代码实现增删改查

```objc
// 打开数据库
[[GKDatabaseManager sharedManager]openDatabase]

// 创建表格
// 默认表为为类名,主键为t_default_id
[[GKDatabaseManager sharedManager] creatTableWithClassName:[Person class]];

// 插入数据
Person * p = [[Person alloc]init];
p.name =@"花菜ChrisCai";
p.age = 100;
[[GKDatabaseManager sharedManager] insertDataFromObject:p]

// 查询指定表内数据
NSArray * persons = [[GKDatabaseManager sharedManager] selecteDataWithClass:[Person class]];

// 模糊查找

// 枚举类型含义
typedef NS_ENUM(NSInteger ,GKDatabaseSelectLocation){
    /// 以某个字符串开头
    GKDatabaseSelectStartWithString = 0,
    /// 包含有某个字符串
    GKDatabaseSelectRangOfString,
    /// 以某个字符串结尾
    GKDatabaseSelectEndWithString
};
// 查询Person表格中所有年龄包含8的
NSArray * resultArr = [[GKDatabaseManager sharedManager] selectObject:[Person class] propertyName:@"age" type:GKDatabaseSelectRangOfString content:@"8"];

// 更新数据
// 将Student表中所有age = 100对应的记录name都改为Chris
[[GKDatabaseManager sharedManager] updateObject:[Student class] oldValues:@[@"age = 100"] conditionType:QueryTypeAND  newValues:@[@"name = Chris"]]

// 指定删除
// 删除Person表中所有age>50的记录
[[GKDatabaseManager sharedManager] deleteObject:[Person class] withString:@"age > 50"]
```
更多详细使用,请看Demo~,
