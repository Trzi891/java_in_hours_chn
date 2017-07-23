# Java编程一天入门

## 目录
(待加)

## 一 准备编程 (建议时间: 20分钟. 如果卡住,请在代码库开issue, 下同)
编程就是让计算机做你想让它做的事.

编程语言是工具,就像画笔,应该拿上手找块空白就可以用.

为了编写第一个Java程序,必需一个Java开发套件(本文代码测试用的是Oracle JDK 8),以及一个写程序的文本编辑工具.
本文的代码足够简单,集成开发环境的用处不大,任何文本编辑器都可以(推荐工具待定.写本文时用的是Komodo Editor免费版).

安装JDK后, 打开命令行窗口,运行javac和java,不报错"command not found",即为成功,可以继续. (待续:常见问题与解决)

扩展资料: 解释器与编译器的区别, JDK(Oracle JDK, OpenJDK), IDE(Eclipse, NetBeans, IntelliJ等等)

## 二 问个好吧 (建议时间: 20分钟)

新建文本文件,命名为"问好.java".输入最简单的一个Java程序:

```
class 问好 {
  public static void main (String[] 参数) {
    // 待续: 要让它做的事
  }
}
```

这个程序定义了一个类(class),名叫"问好",文件名一般与类名相同. 这个类就是一个程序. 里面的main是程序入口. 注意所有的大括号都需要配对. 双斜杠"//"之后的是注释,是为读代码的人方便理解写的,不影响编译运行.
"参数"很扎眼吧,不用急,第四讲就知道它做什么了.

这个程序可以编译运行(见"手把手"部分),但运行后没有任何输出.因为这个程序是个空架子,没有任何可以看到的运行结果.下面就让它做点事.

```
class 问好 {
  public static void main (String[] 参数) {
    // 要让它做的事
    System.out.println("吃了么");
  }
}
```

加上的这行代码将打印一行字,内容是"吃了么".

试试编译运行,将看到命令行下输出:
```
吃了么
```

试试改字符串的内容,再编译运行.恭喜! 你已经可以写出无数个不同的Java程序了.
再试试加一行相同的代码,输出结果变了吗? 恭喜! 你已经可以写出无限长的Java程序了.

### 手把手:
在命令行下编译和运行
#### 编译:
在程序文件的目录下,运行下面的命令
```
$ javac 问好.java
```
此命令将程序文件编译生成.class文件,在这个目录下多了一个"问好.class"文件

注: 在Windows下, 如果报错"unmappable character for encoding GBK", 请加编码参数:
```
$ javac -encoding utf8 问好.java
```
#### 运行
下面的命令寻找并运行叫"问好"的类:
```
$ java 问好
```

## 三 Java的现状 (建议时间: 10分钟)
在更进一步之前,最好了解现在Java都用来做什么.

优点:
- Oracle JDK是开源的, 另有一个社区维护的版本OpenJDK也是.
- 程序员用户群很大, 能碰到的问题基本上都被前人趟过雷了.
- 可以用的成熟的经过时间检验的库很多.

用途:
- 很大一部分网络服务
- 大多数安卓手机应用
- 少量游戏和桌面应用
- 一些企业内部用Java Applet做可以嵌入网页的在线工具. Chrome浏览器已不支持Java Applet,原因之一是安全性

扩展资料: Apache Maven, Java Applet

## 四 用Java算术 (建议时间: 40分钟)

新建文件"四则运算.java"
```
class 四则运算 {
  public static void main (String[] 参数) {
    System.out.println(1+2);
  }
}
```
编译运行后,果然输出3. 再试试其他四则运算吧,加减乘除运算符分别是+-*/.
还有括号也可以用. 注: 如果算式中所有的数都是整数,那么每步运算都会取整

恭喜! 你已经可以用Java程序完成数学运算了.

那么其他的运算呢? 新建文件"根号.java"
```
class 根号 {
  public static void main (String[] 参数) {
    System.out.println(Math.sqrt(4));
  }
}
```
看起来告诉程序的值是4,编译运行后, 果然如愿打印出了2.0. Math.sqrt是Java中开根号的方法.
应该不用啰嗦了,试试把4改成其他的数,看看结果如何?

现在,你可能已经觉得程序的"回答"太"精简"和生硬了,那么人性化一些吧,下面开始只列出main方法内的代码
```
    System.out.println("4的平方根是" + Math.sqrt(4));
```
输出听起来顺耳些了,但如果想要把4改成其他数,需要改程序的两个地方,这种麻烦可要不得! 可以把4先存到一个变量里,然后在两处引用同一个变量:
```
    int 数 = 4;
    System.out.println(数 + "的平方根是" + Math.sqrt(数));
```
这样只要改一处了.不过,为了改输入值,还是要改程序,再编译再运行,这种麻烦可要不得! "参数"终于派上用场了.
```
    int 数 = Integer.parseInt(参数[0]);
    System.out.println(数 + "的平方根是" + Math.sqrt(数));
```
"参数[0]"是"参数"数组的第一个值. Integer.parseInt是Java把字符串转换成整数的方法.
现在代码里没有了输入值,该怎样告诉程序需要给什么数开根号呢?
在运行程序时,命令后加上一个"参数":
```
$ java 根号 4
```
如果忘了在运行时加参数, 这个程序会打印一个异常报告: java.lang.ArrayIndexOutOfBoundsException.
意思是:数组是空的,却要取第一个值,没辙.

试试多加几个参数吧, 参数[1]是"参数"数组第二个值,以此类推.
恭喜! 你的程序不用修改代码就可以接受不同的外部输入了.

Math是Java自带标准库中的数学类,包含很多有用的方法.详细请查阅JDK文档.

标准库有很多有用的类. 比如随机数, 用在很多聊天机器人上.
新建"随机数生成器.java":
```
class 随机数生成器 {
  public static void main (String[] 参数) {
    java.util.Random 生成器 = new java.util.Random();
    System.out.println("来一个随机数:" + 生成器.nextInt());
  }
}
```
java.util.Random是随机数类的全路径, java.util是它所在的包. 没有全路径Java就找不到这个类了.
为什么Math和Integer没有这样的前缀呢? 因为他们在java.lang包里,是"亲生"的,不用包名Java也能找到这些类.

"生成器"是随机数类的一个"个体". 用new关键词来产生. 一个现实的比方: "人"是一个类型, 你我都是同样类型的不同个体.
nextInt是产生一个随机数的方法. 为什么Math.sqrt和Integer.parseInt不用new出一个个体呢? 因为它们和main方法一样, 都是静态(static)的.

这样重复类的全名看着真累, 下面用import来开头导入这个类路径, 之后就不用再重复了:
```
import java.util.Random;

class 随机数生成器 {
  public static void main (String[] 参数) {
    Random 生成器 = new Random();
    System.out.println("来一个随机数:" + 生成器.nextInt());
  }
}
```

扩展资料: 数组, 异常, 方法, JDK文档

## 五 变量-在程序中保存修改信息 (建议时间: 15分钟)

在上一讲的"根号"类中,用了一个整形(int)变量来保存输入值. "参数"是一个字符串(String)数组.
Java中还有其他几种基本变量: boolean, char, byte, short, long, float, double
```
boolean 布尔量 = true; // true或false,真或假
char 字符 = '好'; // 单个字符
byte 字节 = 27; // -128到127, 即-2^7到(2^7-1)
short 短整数 = 12345; // -32768到32767, 即-2^15到(2^15-1)
int 整数 = 1234567890; // -2^31到(2^31-1)
long 长整数 = 123456789000000000l; // -2^63到(2^63-1)
float 单精度浮点数 = 1.1f; // 2^-126到(2-2^-23)*2^127
double 双精度浮点数 = 1.1; // 2^-1074到(2-2^-52)*2^1023
```
它们的范围逐渐增大,可以根据需要选择. 长整数后如果不加'l',会被默认为int值.

上一讲的四则运算类中,已经尝试了4种运算符. 变量运算的结果可以赋给自己,或者另一个变量.

举个例子,某投资方法,可以有8%的年回报率,那么1000元的初始投入资金,3年之后会变成多少.下面是一个很直白的计算方法:
```
class 投资回报 {
  public static void main (String[] 参数) {
    float 账户余额 = 1000f;
    float 回报率 = 0.08f;

    // 第一年
    账户余额 = (1 + 回报率) * 账户余额;

    // 第二年
    账户余额 = (1 + 回报率) * 账户余额;

    // 第三年
    账户余额 = (1 + 回报率) * 账户余额;
    System.out.println("三年后变成" + 账户余额 + "元");
  }
}
```
你的感觉没错, 它看起来就很累赘, 而且如果要算20年后呢?

恭喜! 你已经有了判断代码优劣的直觉. 至于改进方法,留个悬念吧.

## 六 文字 (建议时间: 30分钟)

之前的程序都用文字的形式"回答"结果. 就像现实世界一样, 文字是最经典基本的人机交流方式. 为此Java提供了很多文本处理的方法.

第一讲中的"吃了么"是一个字符串(String). 它由三个字符(char)组成: '吃','了','么'.
注意在定义变量时字符用单引号,而字符串用双引号. 就像上一讲的浮点数后的f和长整数后的l一样, 这些都是Java的"传统". 考虑到Java诞生在上世纪90年代初,就配合一下吧.

可能已经注意到String开头是大写的,没错,和其他基本变量类型不同,它是一个类.

第一讲中也许已经试过了多个System.out.println,每个会打出一行. 如果不想另起一行, 用System.out.print就行.

既然用双引号包起来的就是字符串,那么如果想在字符串里显示双引号,该怎么办呢? 这需要加一个反斜杠: \\"

那么反斜杠又是个特殊符号了, 如果要显示它, 就需要再加一个: \\\\
类似的还有\t(制表符), \n(换行)等等. 如果将来有一个想不出怎么显示的东西, 再找本工具书看看Java特殊字符部分吧. 下面的程序演示一些:
```
class 特殊字符 {
  public static void main (String[] 参数) {
    System.out.println("边检员看了看证件,头没抬地说\t\"这么久没回了啊?\".\n百感交集,不知为何咧着嘴回了一句\t\"是啊,抗战还没完呢\"");
  }
}
```
前几讲已经用过加号连接多个字符串,以及其他类型的变量. 只要是基本变量,都可以这样和字符串用加号连接,产生一个新的字符串.

字符串有不少常用方法,比如获取长度,搜索子字符串,变换英文大小写等等.下面演示他们的用法:
```
class 字符串方法 {
  public static void main (String[] 参数) {
    String 字符串 = "去是go";
    String 搜索字符串 = "go";
    System.out.println("\"" + 字符串 + "\"的长度:" + 字符串.length());
    System.out.println(搜索字符串 + "在\"" + 字符串 + "\"的位置是:" + 字符串.indexOf(搜索字符串));
    System.out.println("\"" + 字符串 + "\"转换为大写是:" + 字符串.toUpperCase());
  }
}
```
扩展资料: 类型转换

## 七 如果...就...不然... (建议时间: 30分钟)
代码说了算:
```
if (年龄 < 20) {
  System.out.println("没到法定婚龄! 等几年再结婚吧");
} else {
  System.out.println("妹妹,真想嫁也拦不住你.要不再考虑一天?");
}
```
if就是"如果",后面跟的是条件, 紧接着的{}在条件满足时执行; else就是"不然",紧接着的{}在之前的条件不满足时执行.
没错, {}里当然可以有多行代码. 然后在if里套if试试?

Java支持所有数学中的大小比较符号: < > >= <=

另外, 因为单个=被用于变量赋值, 判断"等于"就用了双等号: == 不等于呢? !=

如果有并列的多个条件,可以串起来这样写:
```
if (年龄 < 5) {
  System.out.println("这是哪家闺女啊?爸妈在哪儿呢?");
} else if (年龄 < 20) {
  System.out.println("没到法定婚龄! 等几年再结婚吧");
} else {
  System.out.println("妹妹,真想嫁也拦不住你.要不再考虑一天?");
}
```
如果把 <5 和 <20的顺序倒过来:
```
if (年龄 < 20) {
  System.out.println("没到法定婚龄! 等几年再结婚吧");
} else if (年龄 < 5) {
  System.out.println("这是哪家闺女啊?爸妈在哪儿呢?");
} else {
  System.out.println("妹妹,真想嫁也拦不住你.要不再考虑一天?");
}
```
即使是3岁的小朋友也满足<20的条件, 因此会执行输出"没到法定婚龄! 等几年再结婚吧".
是的,计算机执行程序就是这么老(si)实(ban), 执行第一个被满足的条件之后的{}内代码, 而且无视后面所有else的条件判断.

注意,字符串的"等于"判断有自己的方法equals,比大小用compareTo:
```
if ("辛苦".equals("不辛苦")) {
  System.out.println("辛不辛苦无所谓");
} else if ("辛苦".compareTo("不辛苦") > 0){
  System.out.println("辛苦点好");
} else {
  System.out.println("不辛苦好");
}
```

扩展资料: &&, ||, switch, ?:, 字符串比较

## 八 直到...一直... (建议时间: 30分钟)
记得算投资回报的程序么? 如果要算20年, 难道必须重复20行"账户余额 = (1 + 回报率) * 账户余额;"吗? 用脚趾想也不可能吧.

在写代码之前, 不妨先构思一下该怎么算. 多了一个输入值是年限,比如20. 照原来的思路应该是: 每过一年增一次值, 直到过了20年. 这样就需要记着过了多少年. 对计算机来说, 一个变量用来"记"变化的值最合适:
```
for (int 年份 = 0; 年份 < 年限; 年份 = 年份 + 1) {
  账户余额 = (1 + 回报率) * 账户余额;
}
```

同样的循环用while的格式来写是这样:
```
int 年份 = 0;
while (年份 < 年限) {
  年份 = 年份 + 1;
  账户余额 = (1 + 回报率) * 账户余额;
}
```
看起来for循环更紧凑, 也更不容易写错. while循环里,如果忘写了"年份 = 年份 + 1;",可就有趣了,因为年份没有增加, 循环中止条件一直不能满足(0永远小于年限), 代码运行停不下来,俗称"死循环". 而for循环里因为定了"(初始化; 循环条件; 执行语句)"的格式, 少了一项会很扎眼.

如果想要提前结束循环,可以用break. 比方说,想知道啥时候能赚到2000:
```
int 年份 = 0;
while (年份 < 年限) {
  if (账户余额 > 2000) {
    break;
  }
  年份 = 年份 + 1;
  账户余额 = (1 + 回报率) * 账户余额;
}
System.out.println(年份 + "年后变成" + 账户余额 + "元");
```
break执行后,它所在的循环就被打断,程序从循环之后开始执行.

如果想要循环继续执行,但是跳过循环内的部分代码,可以用continue. 一个牵强的例子,如果从第三年才开始有回报:
```
for (int 年份 = 0; 年份 < 年限; 年份 = 年份 + 1) {
  if (年份 < 3) {
    continue;
  }
  账户余额 = (1 + 回报率) * 账户余额;
}
```
注: 有更简短的实现方法, 这个例子只为了演示continue的用处.
恭喜! 至此控制流介绍完了.

扩展资料: 变量初始值, 作用域, ++, --, do...while, 递归(例子见:递归死)

## 九 造个人 (建议时间: 30分钟)

我们都是人类,每个人都是一个个体,大多数人有共有的属性和行为,同时也存在个体之间的差异.
下面就来在程序里定义一个"人"类:
```
public class 人 {
}
```
这样的"人"还什么都做不了. 我们出生后都有姓名,那么它也应该有:
```
public class 人 {
  String 姓名 = "无名氏";
  
  public void 自我介绍() {
    System.out.println("我叫" + 姓名);
  }
}
```
这个类具有了"姓名"属性, "自我介绍"方法引用了这个属性并输出加工后的回答.
class前的public表示"人"可以在其他类里使用. 比如这个"世界"类里, "我"是"人"类的一个个体:
```
class 世界 {
  public static void main(String[] 参数) {
    人 我 = new 人();
    我.自我介绍();
  }
}
```
不过,应该有个像样的名字,而不是默认的"无名氏". 需要在自我介绍之前,先定名字:
```
    我.姓名 = "小白";
```
编译运行"世界"后,可以看到输出.

这个世界好像太单调了,人有不同分类,大人,小孩等等,他们做不同的事.新建"大人"类:
```
public class 大人 extends 人 {
  String 责任 = "扶老携幼";
  
  public void 生活() {
    System.out.println("我必须" + 责任);
  }
}
```
再新建"小孩"类:
```
public class 小孩 extends 人 {
  String 想做的事 = "大人的事";
  
  public void 长大() {
    System.out.println("我要做" + 想做的事);
  }
}
```
现在的世界要喧闹一些了:
```
class 世界 {
  public static void main(String[] 参数) {
    大人 大白 = new 大人();
    小孩 小白 = new 小孩();
    
    大白.姓名 = "大白";
    大白.自我介绍();
    大白.生活();
    
    小白.姓名 = "小白";
    小白.自我介绍();
    小白.长大();
  }
}
```
"大人"和"小孩"都是"人"的扩展类(俗称"子类"), 他们也可以有自己的"子类",比如"婴儿"可以是"小孩"的子类.

扩展资料: 接口(interface)

## 十 让它更像人 (建议时间: 30分钟)

一个人还有很多属性:
```
public class 人 {
  String 姓名 = "无名氏";
  int 年龄 = 0;
  float 身高 = 0.0f;
  private String 小秘密 = "";
  
  public void 自我介绍() {
    System.out.println("我叫" + 姓名 + ", 今年" + 年龄 + "岁");
  }
}
```
谁的小秘密都不可以直接让别人知道. private就限制了这个变量只能给个体内部使用, 任何其他类里,都不能直接获取这个值. 下面这个程序在编译会报错:
```
class 世界 {
  public static void main(String[] 参数) {
    人 我 = new 人();
    System.out.println(我.小秘密);
  }
}
```
既然这个小秘密只能由自己引用和修改, 一般有公开方法可以让其他类间接接触这个变量:
```
public String 回答(String 听到的) {
  if (听到的.contains("?")) {
    return "你猜? 答案长度是" + 小秘密.length();
  } else if (听到的.contains("秘密")) {
    小秘密 = 听到的;
    return "我记住了";
  } else {
    return "...";
  }
}
```
根据"听到的"内容, 如果里面包含问号, 就提示秘密的字符串长度, 让猜秘密. 如果包含"秘密"两个字,就把它存在"小秘密"变量里. 再不然,就...了.

这个方法返回(return)一个字符串. 可以在"世界"类里打印出每个回答.

在创建个体的时候, 之前都是new xxxx(), 没有传入任何参数. 因此如果在创建后对属性初始化就需要这样做:
```
    大人 大白 = new 大人();
    大白.姓名 = "大白";
    大白.年龄 = 30;
```
另一种比较简洁的方法是, 在"大人"类里定义一个带参数的创建方法:
```
  public 大人(String 姓名, int 年龄) {
    this.姓名 = 姓名;
    this.年龄 = 年龄;
  }
```
然后在创建"大人"个体时,就可以这样:
```
大人 大白 = new 大人("大白", 30);
```
同样可以在"小孩"类里定义一个类似的创建方法. 黏贴复制的很愉快吧? 不过每当这样愉快的时候,就需要警惕一下,因为重复的代码往往意味着设计问题,而且很可能增加今后代码维护的难度. 一个不成文的经验是, 重复代码越少越好.

一个思路是, 大人和小孩都是"人",那么这个内容相同的创建方法理应由"人"来定义. 然后"大人"和"小孩"只要引用它就可以了.
具体实现请参考super关键词.

扩展资料: private/protected/public, static, final, set/get

## 十一 数据排排站-数组 (建议时间: 30分钟)

第四讲里, 已经用过了"参数"这个字符串数组. 下面我们用数组给人排队:
```
class 排队 {
  public static void main(String[] 参数) {
    人[] 一队 = {
      new 人("小明",14),
      new 人("小红", 5),
      new 人("大黄", 12),
      new 人("阿牛", 9)
    };
    
    for (int 序号 = 0; 序号 < 一队.length; 序号++) {
      一队[序号].自我介绍();
    }
  }
}
```
"人"是单个的人, 多加一对方括号"人[]"就成了一队人(再加一对[]呢?). "一队"是个长度为4的数组. 它的length属性就是它的长度. 在它初始化时, 长度就已经确定了,而且之后不能修改. 之前我们用过"参数[0]"获得"参数"数组的第一个值. 同样在这里可以用从0到(一队.length-1)的变量"序号"来获取数组里的每个值.

注意: 数组的序号是从0开始的, 这是比Java年纪还大的一个老传统, 再配合一下吧.

数组还有另一种初始化方法:
```
    人[] 二队 = new 人[10];
    二队[0] = new 人("阿狗", 11);
    二队[1] = new 人("阿猫", 10);
    // 2空着
    二队[3] = new 人("阿猪", 9);
```
很直白, 一开始是初始化一个长度是10的数组, 之后就是往数组中的指定位置放个体.

如果对二队按照一队的方式来"报数", 会报错NullPointerException,因为位置2还空着. 这时需要加个"不为空"的判断条件:
```
    for (int 序号 = 0; 序号 < 二队.length; 序号++) {
      if (二队[序号] != null) {
        二队[序号].自我介绍();
      }
    }
```
排了队, 下面就试试按照某个属性排序. 比如要按年龄对一队排序. 大略的思路可能是: 比较相邻的两人年纪,谁小就排在前面. 下面是Java对应这种思路的一种程序:
```
    java.util.Arrays.sort(一队, new java.util.Comparator<人>() {
      @Override
      public int compare(人 甲, 人 乙) {
        return 甲.年龄 - 乙.年龄;
      }
    });
```
Arrays和Comparator都是java.util包里的类. 如果嫌这样不美观可以在程序前import这两个类.

如果想要排个方阵呢? 只要再加一对[]就可以了:
```
人[][] 方阵 = new 方阵[10][15];
方阵[0][0] = new 人("阿狗",3);
方阵[2][4] = new 人("阿猫",4);
```

扩展资料: 排序算法, 泛型

## 十二 更多结构 (建议时间: 40分钟)

数组已经可以做很多事了, 但它的局限在于长度是不可变的. 上一讲的一队里只能"换人",不能加进第五个人了, 而且,即使把位子空出来,"队伍"的长度也还是四.

当然有变通的办法, 比如: 上来就建个够大的,在90%的问题里,可能一百万就够大了,反正内存现在都是几个G的. 或者灵活点, 满了的时候就新建一个更大的数组, 把原本的数据"挪"到新数组里. 很显然, 这两种做法都有前人实践了. 后者明显是更普遍适用的, 于是这套做法在Java 1.2版里(现在有1.9了)就催生了标准库的java.util.ArrayList类.

注: 知道这个由来不是因为我是考古专业,也不是信口胡诌. 记得之前说过JDK是开源的吗? Java标准库当然也是JDK的一部分, 有兴趣的可以看看ArrayList.add方法的实现.

"排队买票.java"演示了它的基本操作. 如果注释还不够清楚的话, 请在代码库开issue质疑.

另一种数据存取方式是根据一类数据,查找另一类数据. 比如说, 九九乘法表, 就是从两个数找对应的结果. 四六二十四可以表示成"46"->24, 二八十六:"28"->16

这种从一种值查询另一种值的情况, 可以考虑哈希表. 示例在"小九九.java".

当然根据思路不同, 一个问题可以用各种不同的结构解决, 比如乘法表用方阵(数组)也合适.

算法和数据结构是程序员面试很喜欢的问题, 因为它很接近数学和建模. 不过实际工作中, 真正需要实现新算法或者改进现有算法的编程工作比例很有限. 即使厌恶数学, 编程也可以做很多很多不需要小学以上数学知识和方法的事情. 当然, 难免有一天会有书到用时方恨少的感觉. 用画画作比方, 二岁的小孩也可以, 毕其一生追求极致也有.

祝涂鸦愉快.

扩展资料: 内存空间占用, 队列(queue), 栈(stack), 树(tree), 图(graph)

## 十三 活久见 (建议时间: 25分钟)

第四讲里, 用到了Integer.parseInt方法. 如果参数输错, 比如"啊呜",运行后会打印出一堆诡异的东西, 其中有NumberFormatException, 也提到"啊呜". 不用懂英文也能猜到这个输入有点问题了.

这个NumberFormatException属于Exception, 俗语叫"异常", 但直译是"例外", 感觉后者的字面意思明确些. 比如这个把字符串转换成整数的方法, "啊呜"对它来说就是个束手无策的例外情况, 拿到手里既然处理不了就会把它"丢"出来. 丢出来就得"接住", 不然像前面那样就砸了. 下面的try ... catch 就是"试试看...接住(例外情况)...":
```
    int 数 = 0;
    try {
      数 = Integer.parseInt(参数[0]);
      System.out.println(数 + "的平方根是" + Math.sqrt(数));
    } catch (NumberFormatException e) {
      System.out.println(参数[0] + "看着不像整数");
      return;
    } finally {
      System.out.println("彩蛋");
    }
```
最后的finally里面可以写无论例外情况还是正常情况都需要运行的内容. "这和不用finally,直接放在后面有啥区别?"

试试不用finally包着运行一个例外情况就知道了. catch里虽然有return, 但程序退出之前还是运行了"彩蛋".

在"人类.回答"方法里丢了一种新建的Exception"听不懂例外". 具体请看"人类","听不懂例外",以及"世界类"中如何接住这个例外并处理的.

扩展资料: Error, (Un)checkedException

## 十四 为人民服务

在chatbot目录中,是一个很简单的聊天机器人和客户端的实现. 机器人回答和第十讲相同. 尚欠细节说明.

编译运行服务器:
```
$ javac chatbot/聊天服务.java
$ java chatbot/聊天服务
服务启动在:http://127.0.0.1:5335/service
```
运行客户端:
```
$ javac chatbot/聊天客户端.java
$ java chatbot/聊天客户端 秘密哦
我记住了
$ java chatbot/聊天客户端 你是谁?
你猜? 答案长度是3
```

扩展资料: JAX-WS, SOAP, REST

## 十五 自我肯定 - 测试

## 零 没有规矩, 不成方圆 - 代码风格 (建议时间: >0)

即使只看一眼, 有个印象就好. 写了一段时间代码之后重温这里也许会有另外的感触.

到现在为止, 代码的写法好像没有什么讲究. 是吗? 回顾一下(注: 凡是规矩必有例外):

1 源码文件
- 文件名和类名相同
- UTF-8编码格式
- 特殊字符: 所有留白(缩进,分隔),都是空格组成的,而不是tab

2 源码结构
- 顺序是: 包声明, 导入语句, 唯一一个类声明
- 导入语句用全路径, 避免使用通配符*. (好像没提过: import java.util.*就是导入所有java.util包下的类. 这样一眼看不出到底导入了哪些类)
- 导入语句的排序. 按照路径名的字符串大小排序, 小的在前面 (比如: "java.util.HashMap"<"java.util.Map"<"java.util.胡诌类")
- 写类文件的时候, 至少, 不能每次新加内容都写在文件最后. 一种规则是,把同类型的语句和代码块放在一起. 比如: 常量在一起,变量在一起,方法在一起,等等. 还有其他"维度"的类型, 比如公有/私有: 公有方法在一起, 私有方法在一起, 等等.

3 语句格式
- {} 就算可以省略, 也写上 (不然更容易犯低级错误, 信不信由你)
- {前不换行,之后换行; }前换行, 之后如果不跟else或者;的话就换行
- 一层缩进是两个空格
- 一行最多一条语句
- 一行语句超过100(?)个字符就分行 (英文代码中超过100读着就太长了,中文代码在表达同样意思时会用更少字符,所以也许100不再恰当了)
- 如何分行呢? 看着顺眼就好 (超出了"入门"的范畴, 改天再详说)
- 空行可以让代码分块显眼. 之前提到的不同类型的语句就可以用空行隔开,比如变量和方法之间. 另外两个方法声明之间也是.
- 空格也可以让代码读起来更容易, 嗯, 再次省去100+字.
- 本地变量(在方法中声明的变量)不到用时不声明 (好处之一是重构起来更方便)
- 数组类型的变量声明时,[]不放在变量名之后 ("人类[] 一队" 和 "人类 一队[]"的语法都允许,但前者看起来更明显是数组)
- switch中, 每个case占单独一行, 如果某个case块有语句, 并且不是以break结束, 需要加上显眼的注释, 表示这是故意而为之的, 比如: // 继续 (等到哪天在switch的一个case忘了break,可能就更能明白用意了)
- 除非case已经包含了所有情况, switch末的default尽量加上, 即使不用处理. (总是想到例外情况,是编程的好习惯)
- Modifier排序: public protected private abstract default static final transient volatile synchronized native strictfp
- 长整型用大写L作后缀,以免小写的l和1太相似

4 命名
- 包名用小写英文或中文, 不用下划线
- 类名尽量用名词或名词短语. 用"类"结尾, 便于和一般变量名区别. 测试类用"测试类"结尾.
- 接口(interface)名用"接口"结尾
- 方法命名尽量用动词开头
- 常量命名以"常量_"作前缀, 注意只用在"真"常量上, 就是初始化后不能被改变的量.
- 类型变量 (待续)

上述代码风格摘自Google Java英文代码风格指南, 加入了一点中文代码相关内容. 删去的列了一些在下面(不完整). 请自行取舍:
- 包和导入语句都是单行 (是的,可以分行写)
- 一个变量一个声明 (int 数一, 数二; 语法允许)
- 英文变量/方法/类名采用骆驼命名法

这么多的规则, 如果没有辅助会增加很多额外负担. 好在现在的集成开发环境(IDE)基本都有根据模板进行代码自动格式化的功能. 善其事, 利其器. 请自行选择一个好用的Java集成开发环境.

江湖再见.

(全文完)

待定:

## 分身有术-多线程

## 文字到图形

## 读写文件

## 内部类, closure, lambda
