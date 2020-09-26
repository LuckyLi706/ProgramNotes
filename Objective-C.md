# 一、基础

## 1.1 日志输出

```objective-c
// NSLog用于日志的输出
NSLog(@"Hello, World!");  //直接输出字符串

//NSLog(@"格式化",变量); 格式化类型类似于c语言
NSLog(@"%i",a);  //输出int类型的变量
NSLog(@"%lx",b);  //输出long类型的变量  
NSLog(@"%c",c); //输出char类型的变量
NSLog(@"%f",d); //输出float类型的变量
NSLog(@"%lg",e);  //输出double类型的变量
NSLog(@"%@",c);  //输出对象类型的变量

```

## 1.2 #import指令

- 增强版的#include指令，和include差不多
- #import<>引入系统相关的类，#import “ ”表示引入非系统相关的类，

## 1.3 条件判断和循环

### 1.3.1 条件判断

```objective-c
//oc的条件和其他语言苍差不多类似，除了false和0为假外，其他都为真
if(判断语句){
   //执行逻辑
}else{
   //其他情况下执行的逻辑
}
```

### 1.3.2 循环

```objective-c
/*
     循环和其他语言差不多类似
     for循环
     语法：
     for (表达式1;表达式2;表达式3) {
      表达式4
     }
     1.初始值
     2.循环判断条件
     3.自增或者自减
     4.循环体

     while循环
     语法：
     while (表达式) {
     循环体
     }

     do while循环
     语法:
     do {
     循环体
     } while (表达式);

     //先循环一次，再执行循环条件，如果为真，接着执行循环体，直到循环条件为假时候跳出循环
*/
//例子：
    //求1-10的和
        NSInteger a = 0;
        for(int i=1;i<11; i++) {
            a = a+i;
        }
        NSLog(@"a = %ld",a);
   //while
        int c = 0;
        NSInteger b = 0;
        while(c<=10) {
            b=b+c;//b+=c;
            c++;
        }
        NSLog(@"b = %ld",b);

        int sum = 0;
        NSInteger f = 0;
        do {
            sum+=f;
            f++;
        } while(f<11);
        NSLog(@"sum = %d",sum);


        //breakcontinune
        NSInteger sum1 = 0;
        for(int j=0;j<=10; j++) {
            if(j==5){
//                break;
                continue;
            }
            sum1 +=j;
        }
        NSLog(@"sum1 = %ld",sum1);

    /*
     while和do while循环用于知道循环结束的条件情况下
     for（；；）用于知道循环次数

     三种情况可以相互转换

     break 和 continue
     break 表示终止本层循环
     continue 表示终止本次循环，进入到下次循环
     */

```

# 二、变量类型

## 2.1 数字类型

```objective-c
/**
1、int、NSInteger、NSNumber区别
int,long,NSInteger,NSLong等都是基本数据类型,
NSNumber是数据对象,可以使用NSNumber数据对象来创建和初始化不同类型的数字对象
NSInteger会根据系统的位数（32or64）自动选择int的最大数值（int or long）,官方推荐使用NSInteger
2、NSUInteger
3、@1  //表示NSNumber类型对象
**/
//第一种转换方式
        //long，double，char，float类似
        NSInteger a=6;
        NSNumber *b=[NSNumber numberWithInt:6];  //创建int类型的对象，通过numberWithXXX也可以创建其他数据类型
        
        if(a == [b intValue]){  //intValue将对象转为基本类型
            NSLog(@"true");
        }
        else{
            NSLog(@"false");
        }
//返回为true

//第二种转换方式
        NSNumber *a=@1;  //直接使用@符号来定义NSNumber对象类型
        NSInteger b=3;
        NSNumber *c=@(b);  //将基本数据类型转为NSNumber对象类型
        NSLog(@"%@,%@",a,c);
```

## 2.2 字符串类型

```objective-c
/**
1、字符串前面都需要加@，如定义字符串: NSString *str=@"abc"  //定义一个abc的字符串
2、NSString为不可变字符串
常用方法：
**/

#pragma mark 初始化字符串
void initStr() {
    //1.init
    NSString *str1 = [[NSString alloc ]init];//不可改变的空字符串 无意义
    NSString *str2 = [NSString string];
    NSLog(@"%@-----%@", str1, str2);
    //2.格式化的方式来创建字符串
    NSString *str3 = [[NSString alloc] initWithFormat:@"%iAA",2];
    NSString *str4 = [NSString stringWithFormat:@"%iBB", 3];
    NSLog(@"%@-----%@", str3, str4);
    //3.快捷方式
    NSString *str5 = @"QWE";
    NSLog(@"%@", str5);
    
}
#pragma mark 从文件中获取字符串
void getStrFromFile() {
    NSString *str = [NSString stringWithContentsOfFile:@"/Users/lanou3g/Desktop/a.txt" encoding:NSUTF8StringEncoding error:nil];
    NSLog(@"%@", str);
}
#pragma mark 字符串写入文件
void setStrInFile() {
    NSString *str = @"ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    NSError *error ;
    [str writeToFile:@"/Users/lanou3g/Desktop/a.txt" atomically:YES encoding:NSUTF8StringEncoding error:&error];
    if (error)
        NSLog(@"文件写入失败%@", [error localizedDescription]);
    else
        NSLog(@"文件写入成功");
}

#pragma mark 获取字符串长度
void getStrLength() {
    NSString *str = @"赵延伟";
    str = @"AA";
    NSInteger length = [str length];//1返回的字符个数
    NSLog(@"length = %zi", length);//3
    
    length = [str lengthOfBytesUsingEncoding:NSUTF8StringEncoding];//2 返回指定编码的字节数 （针对汉字）
    NSLog(@"length = %zi", length);//9
    
    length = [str maximumLengthOfBytesUsingEncoding:NSUTF8StringEncoding];//3 返回字节存储接收器在给定的编码所需的最大数目（不知所云）
    NSLog(@"length = %zi", length);
}

#pragma mark 获取字符
void getChar() {
    NSString *str = @"ABC";
    char ch = [str characterAtIndex:1];//根据索引获取字符 ch = c
    
 //  [str getCharacters:'C' range:NSMakeRange(0, 1)];//？？？
    NSLog(@"%c",ch);
}

#

#pragma mark 获取C语言的字符串
void getCStr() {
    NSString *str = @"AAAABBC";
    const char *ch1 = [str UTF8String];//不可变的
    NSLog(@"%s",ch1);
    
  //  BOOL b= [str getCString:"12" maxLength:7 encoding:NSUTF8StringEncoding];不明确
    
    const char *ch2 = [str cStringUsingEncoding:NSUTF8StringEncoding];
    NSLog(@"%s",ch2);
    //NSLog(@"%@", str);
    
}

#pragma mark 拼接字符串
void appendStr() {
    NSString *str = @"AAA";
    NSString *temp = @"BB";
    //1
    NSLog(@"%@", [str stringByAppendingString:temp]);
    //2
    NSLog(@"%@", [str stringByAppendingFormat:@"%iKFC%.2f", 8, 3.14]);
    //3 参数说明 第一个返回的字符串长度 第二个是 追加的字符串 第三个是追加字符串的索引值
    str = [str stringByPaddingToLength:9 withString:@"233" startingAtIndex:2];
    NSLog(@"%@", str);
}

#pragma mark 拆分字符串
void didStr() {
    NSString *list = @"Karin, Carrie, David";
    NSArray *listItems = [list componentsSeparatedByString:@", "];
    NSLog(@"%@",listItems);
    
    NSString *str = @"ABCDEFGHI";
    str = [str substringFromIndex:2];//包括当前位置
    
    NSLog(@"%@",str);
    str = [str substringToIndex:6];//不包括当前位置
   
    NSLog(@"%@",str);
    str = [str substringWithRange:NSMakeRange(1, 3)];
    
    NSLog(@"%@",str);
}

#pragma mark 查找字符串
void findStr() {
    NSString *str = @"1234AAA5678";
    NSRange range = [str rangeOfString:@"AAA"];
    NSLog(@"%@", NSStringFromRange(range));
    
    range = [str rangeOfString:@"AAA" options:1];//1表示并行
    NSLog(@"%@", NSStringFromRange(range));
    
    range = [str rangeOfString:@"AAA" options:1 range:NSMakeRange(0, 6)];
    NSLog(@"%@", NSStringFromRange(range));//不存在时候 判断 range.length == 0
}
#pragma mark 替换字符串
void replaceStr() {
    NSString *str = @"1234AAA5678";
    str = [str stringByReplacingOccurrencesOfString:@"AAA" withString:@"BBB"];
    str = [str stringByReplacingCharactersInRange:NSMakeRange(6, 3) withString:@"CCC"];

    NSLog(@"%@", str);
}
```

## 2.3 布尔类型

```objective-c
/**
1. 布尔可以当做整型来用；BOOL YES NO全部是大写，没有小写；
2. 布尔类型的本质：typedef signed char BOOL;
3. 输出是YES或者NO，还有1和0
**/
BOOL d=TRUE;
if(d){
     NSLog(@"true");
}
else{
     NSLog(@"false");
}
//输出true
```

## 2.4 数字类型和字符串类型转换

```objective-c
NSString *newString="abc";
// 字符转int
int intString = [newString intValue];
// int转字符
NSString *stringInt = [NSString stringWithFormat:@"%d",intString];

// 字符转float
float floatString = [newString floatValue];
// float转字符
NSString *stringFloat = [NSString stringWithFormat:@"%f",intString];
```

# 三、变量类型二

## 3.1 数组类型

### 3.1.1 不可变数组NSArray

```objective-c
/**
1、不可存放基本数据类型，只能存放oc对象
2、可以存放多种对象类型的数据
3、一旦创建成功,内容不可改变
**/

//初始化操作
    //1)创建一个空数组
    NSArray *arr1 = [NSArray array];

    //2)创建数组,只有一个元素
    NSArray *arr2 = [NSArray arrayWithObject:@"1"];

    //3)创建数组,有多个元素
    // nil 表示数组赋值结束
    // 常见写法
    NSArray *arr3 = [NSArray arrayWithObjects:@"one",@"two",@1, nil];
                    NSLog(@"arr3 = %@",arr3);
    //4)调用对象方法,创建数组
    //nil Nil NULL  NSNULL
    NSArray *arr4 = [[NSArray alloc] initWithObjects:@"three",[NSNull null],@"four", nil];
                    NSLog(@"arr4 = %@",arr4);
    //5)用一个数组可以创建另外一个数组
    NSArray *arr5 = [NSArray arrayWithArray:arr3];


//基本使用
    NSArray *arr3 = [NSArray arrayWithObjects:@"one",@"two",@1,@"three", nil];
    NSLog(@"arr3 = %@",arr3);

    //1)获取数组的长度  count获取数组的元素的个数
    NSLog(@"%ld",arr3.count);

    //2)根据下标,获取下标对应的对象
    NSLog(@"%@",[arr3 objectAtIndex:3]);

    //3)返回元素的下标
    NSUInteger loc = [arr3 indexOfObject:@"three"];
    NSLog(@"%ld",loc);

    //4)数组中是否包含了某个元素
    if([arr3 containsObject:@"four"]){
       NSLog(@"包含此元素");
    }else{
       NSLog(@"不包含");
    }


//简化形式
    //用简化的方式,来定义和访问数组元素
    //1)用简化的方式,定义数组
    //格式: @[ 数组元素 ]
    NSArray *arr = @[@"1",@"one",@"3",@4,@"ONE"];
    NSLog(@"arr = %@",arr);
    
    NSString *str =[arr objectAtIndex:2];
    NSLog(@"%@",str);
    
    //2)用简化的方式访问数组元素
    str = arr[1];   //C语言形式的数组元素访问
    NSLog(@"%@",str);
```

#### 3.1.1.1 遍历

```objective-c
    //定义一个数组
    NSArray *arr = @[@"one",@"two",@"three",@"four"];
    
    //对数组进行遍历
    
    //1) 普通的方式,通过下标访问
    for (int i=0; i<arr.count; i++) {
        NSLog(@"-> %@",arr[i]);
    }
    
    //2) 快速枚举法 for循环的增强形式
    for (NSString * str in arr) {
         NSLog(@"---> %@",str);
    }
    

    //3) 使用block的方式,进行访问(目前还未理解该方式)
    //                               数组元素            元素下标     是否停止
    //stop:YES  会停止, stop:NO 不会停止
    [arr enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop) {
        if(idx == 2){
           *stop = YES;  //停止  // break;     
        }else{
           NSLog(@"idx = %ld,obj = %@",idx,obj);
        }
    }];
```

#### 3.1.1.2 文件读写

```objective-c
//将NSArray写入文件
   NSArray *array = [NSArray arrayWithObjects:@"one",@"zbz",@"cgx",@"sb",@"cjk",@"senni", nil];
   //把NSArray 中的内容,写入到文件中
   //arr.plist 一种特殊的文件格式
   BOOL isWrite =  [array writeToFile:@"/Users/zhaoxiaohu/Desktop/arr.xml" atomically:YES];
   if(isWrite){
      NSLog(@"写入成功");
   }

//从文件中读取NSArray对象
  NSArray *readArr = [NSArray arrayWithContentsOfFile:@"/Users/zhaoxiaohu/Desktop/arr.xml"];
  NSLog(@"readArr = %@",readArr);
```

#### 3.1.1.3 拼接成字符串和拆分成NSArray

```objective-c
//将数组拼接成字符串
  
  //1)需求: 把数组中的元素用 "-" 连接起来
  //  [数组 componentsJoinedByString @"分隔符"];
  // 1-2-3-4
  NSString *str = [arr componentsJoinedByString:@"-"];
  NSLog(@"str = %@",str);

//将字符串拆分成数组
  //2) 给一个字符串,分割成一个数组
  // 400-800-12580 //取得 400 12580 800
  NSString *str2 = @"400-800-12580";
  NSArray *arr2 = [str2 componentsSeparatedByString:@"-"];
  NSLog(@"%@",[arr2 firstObject]);  
  NSLog(@"%@",[arr2 lastObject]);
  NSLog(@"%@",arr2[1]);
```

### 3.1.2 可变数组NSMutableArray

```objective-c
1、可变数组，继承于不变数组NSArry；
2、不可变数组的方法都可以用于可变数组

//初始化
  //创建一个空的可变数组
  NSMutableArray *arr = [[NSMutableArray alloc]init];
  //给一个初始化容量
  NSMutableArray *arr1 = [[NSMutableArray alloc]initWithCapacity:10];
  //类方法
  NSMutableArray *arr2 = [NSMutableArray array]
    
//添加元素
   NSArray *arr = @[@“zjp”,@“ww”,@“jjj”,@“ww”,@“ahk”];
   NSMutableArray *arr1 = [[NSMutableArray alloc]init];
   NSMutableArray *arr2 = [NSMutableArray array];//类方法 
   //增加一个对象
   [arr1 addObject:@"jay"];
   //从数组里增加对象元素
   [arr1 addObjectsFromArray:arr];
   NSLog(@"arr1= %@",arr1);
   //插入
   //插入元素 在指定的下标位置
   [arr1 insertObject:@"hello" atIndex:0];

//删除元素
   //删除 指定下标的元素
   [arr1 removeObjectAtIndex:0];
   NSLog(@"arr1= %@",arr1);
        
   //删除最后 一个元素
   [arr1 removeLastObject];
   NSLog(@"arr1= %@",arr1);
        
   //删除指定元素 如果你数组里有多个相同的元素，也会一起删除
   [arr1  removeObject:@"ww"];
   NSLog(@"arr1= %@",arr1);
        
    //删除指定范围的 元素
    NSRange range = {0,2};
    [arr1 removeObject:@"zjp" inRange:range];
    NSLog(@"arr1= %@",arr1);
        
    //删除指定范围里的 所有元素
    [arr1 removeObjectsInRange:range];
    NSLog(@"arr1= %@",arr1);
        
    //删除指定数组的所有元素
    [arr1 removeObjectsInArray:@[@"zjp"]];
    NSLog(@"arr1= %@",arr1);
        
    //删除指定下标集合的元素
    //下标集合类
    NSMutableIndexSet *indexSet = [[NSMutableIndexSet alloc]init];
    [indexSet addIndex:0];//把下标0放进集合里
    [indexSet addIndex:1];//把下标2放进集合里
    [arr1 removeObjectsAtIndexes:indexSet];
    NSLog(@"arr1= %@",arr1);
        
    //删除数组的所有元素
    [arr1 removeAllObjects];
    NSLog(@"arr1= %@",arr1);

//元素交换
    NSMutableArray *array = [NSMutableArray arrayWithObjects:@"1",@"2",@"3",@"4",@"5",nil]
    //交换元素
    //交换指定下标的数组元素
    NSLog(@"array= %@",array);
    [array exchangeObjectAtIndex:0 withObjectAtIndex:4];
    NSLog(@"array= %@",array);
        
    //替换指定下标的元素   
    [array replaceObjectAtIndex:4 withObject:@"6"];
    NSLog(@"array= %@",array);
```

### 3.1.3 NSSet

```objective-c
/**
1、NSSet集合其实和NSArray集合很类似，只不过NSArray集合时有序的，NSSet集合是无序的。
2、这个方面是和java中的Set是类似的。
3、NSSet和我们常用NSArry区别是：在搜索一个一个元素时NSSet比NSArray效率高，主要是它用到了一个算法hash(散列，也可直译为哈希)
**/
```

## 3.2 字典类型

### 3.2.1 不可变字典NSDictionary

```objective-c
//初始化操作    
    NSDictionary *dic=[NSDictionary dictionaryWithObject:@"卢灿小样" forKey:@"lucan"];
    NSLog(@"%@",dic);
    NSLog(@"%@",[dic objectForKey:@"lucan"]);
    //输出dic键值对个数
    NSLog(@"%d",dic.count);
    
    //用多种方法创建键值对
    NSDictionary *dic1=[NSDictionary dictionaryWithObject:@"卢灿实验2号" forKey:@"小样"];
    NSLog(@"%@",[dic1 objectForKey:@"小样"]);
    
    NSDictionary *dic2=@{@"first":@"2301",@"sec":@"2034"};
    NSDictionary *dic3=[NSDictionary dictionaryWithObjectsAndKeys:@"刘湘",@"name",@"小样",@"name1", nil];
    //输出结果
    NSLog(@"  ----%@%@",dic2,dic3);
    
    //数组把vaule和key放到一个可变数组
    NSArray *values=@[@123,@668,@345];
    NSArray *key=@[@"first",@"swcond",@"third"];
    NSDictionary *dic4=[NSDictionary dictionaryWithObject:values forKey:key];
    NSLog(@"xxxxxxxxxxxx%@",dic4);

    //用一个现有字典对象初始化另一个新字典对象(创建可变对象)
    NSDictionary *arry1=[[NSDictionary alloc]initWithDictionary:dic4 ];
    NSLog(@"ooooooo%@",arry1);
```

#### 3.2.1.1 遍历

```objective-c
    //字典的遍历key1相当于a[i]中的i，dic4就自己定义的字典
    for (id key1 in dic4) {
        id vaule=[dic4 objectForKey:key1];
        NSLog(@"qqqqqq%@%@",key,vaule);
    }
```

#### 3.2.1.2 文件读写

```objective-c
    //保存对象到内容文件
    NSString *path=@"/Users/apple/Desktop/test.plist";
    [dic2 writeToFile:path atomically:YES];
    
    //从以前保存的文件读取到字典对象
    NSDictionary *data=[NSDictionary dictionaryWithContentsOfFile:path];
    NSLog(@"xxxxx%@",data);
```

### 3.2.2 可变字典NSMutableDictionary

```objective-c
    //删除键值对
    NSMutableDictionary  *dic7=[NSMutableDictionary dictionaryWithDictionary:dic2];
    [dic7 removeObjectForKey:@"sec"];
    NSLog(@"%@",dic7);
    
    // 判断key值有就替换没有就添加
    [dic7 setObject:@"3412" forKey:@"sec"];
    NSLog(@"%@",dic7);
    
    //增加dic4  字典无顺序
    [dic7 addEntriesFromDictionary:dic4];
    NSLog(@"%@",dic7);
```

# 四、类

### 

