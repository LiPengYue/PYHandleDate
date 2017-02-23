# PYHandleDate
很好用的时间处理类，可以字符串转时间对象，也可以两个对象（可以转成时间对象的OC对象）比较，返回时间差，并拆分时间差成年月日....
#前言：
>终于找到了工作，不是科班出身，找工作还真的很不容易，工作中遇到了时间转化成字符串（时间差转成字符串）并显示，于是写了一个工具类，在此与大家分享，如果感觉还方便，请点个赞~

##设计模式：
>考虑到了要多次使用这个类，而且初始化`NSDateFormatte` 会比较耗时，所以采用了单利模式。
```
//单利
+ (instancetype) sharedHandleDate;
```

---
##参数说明：

**1. NSObject对象 参数**
>1. `NSString`   你可以传一个字符串，但是这个字符串必须是以下两种类型
>
| NSString              |dateFormatter            |  
| :-------- :           | :--------:              |
| @"2017-9-29 0:0:00”   | @"yyyy-MM-dd HH:mm:ss”  |
| @“2017 : 2 : 2”       | @“yyyy : MM : dd”       |
| @“123456”             | @"yyyy-MM-dd HH:mm:ss”  |
|@“2017年12月12日”      |@“yyyy年MM月dd日”         |
|注意传入的分隔符一定要与DateFormatte的分隔符一至|
2.`NSNumber` （这个没有要求传入@(1231234) dateFormatte可以是任意）

---
#方法说明：

**1.对象转化成时间**
```
/**
 * 关于对象转化成对象的方法
 * date_OBJ: 一个对象
 * 如果 转化失败，那么返回nil，并打印无法转化
 */
- (NSDate *)returnDateWithOBJ: (NSObject *)date_OBJ andDateFormatter: (NSString *)dateFormatterStr;
```


**2 .比较早晚**
>1.比较早晚 返回bool值
```
/**
 * 关于时间与当前时间 比较早晚 的方法
 * date_OBJ : 传入一个字符串或者时间对象
 */
- (BOOL)isLateCurrentDateWithDate: (NSObject *)date_OBJ andDateForMatter: (NSString *)dateForMatter andIsDateStr: (BOOL)isDateStr;
```
>2.返回NSDate对象
```
/**返回较晚的时间*/
+ (NSDate *)laterDateWithData: (NSObject *)date andOtherDate: (NSObject *)otherDate andCompareType: (PYHandleCompareType)compareType;
```


**3.时间拆分成 年、月、日..并返回** 
>对象分隔成年月日时分秒 用block进行参数的返回
```
/**
 * 传入一个对象 获取对应的时间
 * date 对象（将被转化成时间对象）
 * dateFormatter 时间格式
 * dateBlock 转化成时间后的年月日
 */
#pragma mark - 获取时间的年月日
- (void)getDate: (NSObject *)getDate andDateFormatter: (NSString *)dateFormatter andDateBlock: (void(^)(NSInteger year, NSInteger month, NSInteger day, NSInteger hour,NSInteger minute, NSInteger second))dateBlock;
```

**4.时间比较，拆分成 年、月、日…并返回**
```
/**
 * 关于两个时间差的方法
 * CompareDate: 比较的 第一个时间
 * forcedCompareDate: 比较的第二个时间
 * block返回的是第一个时间 减去第二个时间
 * 返回值是 差的时间；
 */
#pragma mark - 两个时间相比的差值
- (NSString *)compareDateWithandDateFormatter: (NSString *)dateFormatterStr andCompareDate: (NSObject *)startTime andSecondCompareDate: (NSString *)endTime andDateBlock: (void(^)(NSInteger year, NSInteger month, NSInteger day, NSInteger hour,NSInteger minute, NSInteger second))dateBlock;
```

[点击这里查看 liYaoPeng 的简书](http://www.jianshu.com/p/00ebd07648ec)
