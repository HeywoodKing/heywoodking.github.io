---
title: python 知识集锦
date: 2020-01-05 23:49:26
tags:
    - IT技术
    - python
    - 知识点
categories: python
type: tags
---


##爬虫

1. TCP/IP模型，TCP协议原理，IP协议原理，TCP三次握手，四次挥手

2. HTTP协议原理

3. HTTP1.1和HTTP2.0区别？

4. python多进程，多线程，协程开发（gevent, asyncio, greenlet）

5. Scrapy框架原理以及分布式爬取

6. Selenium框架原理，WebDriver

7. 解析工具Jsoup, Xpath, Beautifulsoup, htmpparser,正则, Nutch, Heritrix

+ Jsoup:

Beautifulsoup for Java
Jsoup就是java环境下同样具有html文档解析的最好的选择之一
主要方法就是 Jsoup.parse()，解析出来的是一个Document对象。Element对象则提供了一系列类似于DOM的方法来查找元素，抽取并处理其中的元素。


+ Xpath:

XPath 是一门在 XML 文档中查找信息的语言。XPath 可用来在 XML 文档中对元素和属性进行遍历。XPath 是 W3C XSLT 标准的主要元素，并且 XQuery 和 XPointer 都构建于 XPath 表达之上。因此，对 XPath 的理解是很多高级 XML 应用的基础


+ Beautifulsoup：

BeautifulSoup库通俗来说是【解析、遍历、维护“标签树”(例如html、xml等格式的数据对象)的功能库】
有五种基本元素：Tag  Name Attributes NavigableString Comment


+ htmpparser:

htmlparser是一个功能比较强大的网页解析工具，主要用于 html 网页的转换(Transformation) 以及网页内容的抽取 (Extraction)。


+ 正则：
正则表达式（regular expression）就是用一个“字符串”来描述一个特征，然后去验证另一个“字符串”是否符合这个特征。比如 表达式“ab+” 描述的特征是“一个 'a' 和 任意个 'b' ”，那么 'ab', 'abb', 'abbbbbbbbbb' 都符合这个特征。

正则表达式可以用来：（1）验证字符串是否符合指定特征，比如验证是否是合法的邮件地址。（2）用来查找字符串，从一个长的文本中查找符合指定特征的字符串，比查找固定字符串更加灵活方便。（3）用来替换，比普通的替换更强大。


+ Nutch:
Nutch 是一个开源Java实现的搜索引擎。它提供了我们运行自己的搜索引擎所需的全部工具。包括全文搜索和Web爬虫。Nutch目前最新的版本为version v2.3


+ Heritrix:
Heritrix是一个由Java开发的开源Web爬虫系统，用来获取完整的、精确的站点内容的深度复制，具有强大的可扩展性，运行开发者任意选择或扩展各个组件，实现特定的抓取逻辑,Heritrix采用了模块化的设计，用户可以在运行时选择要用的模块。它由核心类（core classes）和插件模块（pluggable modules）构成。

核心类可以配置，但不能被覆盖，插件模块可以由第三方模块取代。所以我们就可以用实现了特定抓取逻辑的第三方模块来取代默认的插件模块，从而满足自己的抓取需要


8. 爬虫策略，反爬虫策略
+ 爬虫策略:
```
- 爬虫的宽度优先抓取策略
宽度优先抓取策略，一个历史悠久且一直被关注的抓取策略，从搜索引擎爬虫诞生至今一直被使用的抓取策略，甚至很多新的策略也是通过这个作为基准的。

宽度优先抓取策略是通过待抓取URL列表为基准进行抓取，发现的新链接，且判断为未抓取过的基本就直接存放到待抓取URL列表的末尾，等待抓取
- 爬虫的深度优先抓取策略
深度优先抓取的策略是爬虫会从待抓取列表中抓取第一个URL，然后沿着这个URL持续抓取这个页面的其他URL，直到处理完这个线路后，再从待抓取的列表中，抓取第二个，以此类推
- 爬虫的非完全PageRank抓取策略
非完全pagerank抓取策略，就是基于在爬虫不能看到所有网页指向某一网页的链接，而只能看到部分的情况，还要进行pagerank的计算结果,
具体策略就是对已经下载了的网页，加上待抓取的URL列表里的网页一起，形成一个汇总。在这个汇总内进行pagerank的计算。在计算完成后，待抓取的url列表里的每一个url都会得到一个pagerank值，然后按照这个值进行倒序排列。先抓取pagerank分值最高的，然后逐个抓取
- 爬虫的OPIC抓取策略
OPIC是online page importance computation的缩写,爬虫把互联网上所有的URL都赋予一个初始的分值，且每个URL都是同等的分值。每当下载一个网页就把这个网页的分值平均分摊给这个页面内的所有链接。自然这个页面的分值就要被清空了。而对于待抓取的URL列表里（当然，刚才那个网页被清空了分值，也是因为它已经被抓取了），则根据谁的分值最高就优先抓取谁
- 爬虫抓取的大站优先策略
爬虫会根据待抓取列表中的URL进行归类，然后判断域名对应的网站级别。例如权重越高的网站所属域名越应该优先抓取
爬虫将待抓取列表里的URL按照域名进行归类，然后计算数量。其所属域名在待抓取列表里数量最多的优先抓取
```
+ 反爬虫策略:
```
- 目前比较常规单有效的手段，比如：
User-Agent + Referer检测
账号及Cookie验证：服务器对每一个访问网页的人都set-cookie，给其一个cookies，当该cookies访问超过某一个阀值时就BAN掉该COOKIE，过一段时间再放出来，当然一般爬虫都是不带COOKIE进行访问的，可是网页上有一部分内容如新浪微博是需要用户登录才能查看更多内容。限制每个每天下载300张.
验证码：当某一用户访问次数过多后，就自动让请求跳转到一个验证码页面，只有在输入正确的验证码之后才能继续访问网站
IP限制频次
javascript渲染：网页开发者将重要信息放在网页中但不写入html标签中，而浏览器会自动渲染<script>标签中的js代码将信息展现在浏览器当中，而爬虫是不具备执行js代码的能力，所以无法将js事件产生的信息读取出来
ajax异步传输：访问网页的时候服务器将网页框架返回给客户端，在与客户端交互的过程中通过异步ajax技术传输数据包到客户端，呈现在网页上，爬虫直接抓取的话信息为空
页面懒加载
Referer字段反爬，请求头字段里需要携带Cookie、User-Agent、Referer等多个字段共同请求才可以获取到图片数据，否则不返回数据
延时操作
网页iframe框架嵌套：在下载框处再内嵌一个窗口，使得爬虫提取不到内层窗口的数据
csrf防护：将图片下载改为post提交，并携带随机的crfs_token值，每次进行比对token值正确后，再返回图片
下载图片返回包含图片得压缩包
限制每日下载量
图片加水印或者logo
DDOS防护
- FONT-FACE拼凑式
猫眼电影里，对于票房数据，展示的并不是纯粹的数字,页面使用了font-face定义了字符集，并通过unicode去映射展示。也就是说，除去图像识别，必须同时爬取字符集，才能识别出数字，并且，每次刷新页面，字符集的url都是有变化的，无疑更大难度地增加了爬取成本
- BACKGROUND拼凑式
与font的策略类似，美团里用到的是background拼凑。数字其实是图片，根据不同的background偏移，显示出不同的字符，并且不同页面，图片的字符排序也是有区别的。不过理论上只需生成0-9与小数点，为何有重复字符就不是很懂
- 字符穿插式
某些微信公众号的文章里，穿插了各种迷之字符，并且通过样式把这些字符隐藏掉。这种方式虽然令人震惊…但其实没有太大的识别与过滤难度，甚至可以做得更好，不过也算是一种脑洞吧
- 伪元素隐藏式
汽车之家里，把关键的厂商信息，做到了伪元素的content里。这也是一种思路：爬取网页，必须得解析css，需要拿到伪元素的content，这就提升了爬虫的难度
- 元素定位覆盖式
还有热爱数学的去哪儿，对于一个4位数字的机票价格，先用四个i标签渲染，再用两个b标签去绝对定位偏移量，覆盖故意展示错误的i标签，最后在视觉上形成正确的价格，这说明爬虫会解析css还不行，还得会做数学题
- IFRAME异步加载式
网易云音乐页面一打开，html源码里几乎只有一个iframe，并且它的src是空白的：about:blank。接着js开始运行，把整个页面的框架异步塞到了iframe里面，不过这个方式带来的难度并不大，只是在异步与iframe处理上绕了个弯（或者有其他原因，不完全是基于反爬虫考虑），无论你是用selenium还是phantom，都有API可以拿到iframe里面的content信息
- 字符分割式
在一些展示代理IP信息的页面，对于IP的保护也是大费周折，他们会先把IP的数字与符号分割成dom节点，再在中间插入迷惑人的数字，如果爬虫不知道这个策略，还会以为自己成功拿到了数值；不过如果爬虫注意到，就很好解决了。
- 字符集替换式
同样会欺骗爬虫的还有去哪儿的移动版，html里明明写的3211，视觉上展示的却是1233。原来他们重新定义了字符集，3与1的顺序刚好调换得来的结果
```

9. 验证码破解


10. mysql数据库原理
> 特点：适用于大中小型网站， 体积小，速度快，总体成本低，开放源代码
mysqld三层结构：
- 连接层：
    + 提供链接协议（TCP/IP socket）
    + 验证功能（用户身份信息）
    + 提供一个专门的连接线程（接受用户发来的sql语句，并在执行后返回最终结果，但不能读和执行sql语句，会将sql语句传递给下一层）
- sql层
    + 接受上层传入的sql
    + 语法检查模块进行语法检查
    + 语义检查模块检查语义，分辨sql语句的类型，将不同种类的语句，交给不同的解析器
    + 解析器接收到sql语句，进行解析操作，得到sql语句的执行计划（explain）
    + 优化器负责基于"开销"找到执行开销最小的执行计划（优化sql，让优化器选择最优的执行方式，了解优化器的规则）
    + 执行器基于优化器的选择，执行SQL语句，并得到获取数据的方法，交给下一层继续处理
    + 接受存储引擎层获取到的二进制数据，结构化成表
    + 查询缓存：SQL语句的哈希值+数据结果（在修改类业务很多的情况下，并不适用）
- 存储引擎层
    + 根据上一层获取数据的方法，将数据提取出来
    + 重新再交给sql层

权限分类：
```
ALL privileges（所有权限）
SELECT, INSERT, UPDATE, DELETE, CREATE, RELOAD, 
SHUTDOWN, PROCESS, FILE, REFERENCES, INDEX, ALTER, 
SHOW DATABASES, SUPER, CREATE TEMPORARY TABLES, DROP
LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT,
CREATE VIEW, SHOW VIEW, CREATE ROUTINE,
ALTER ROUTINE, CREATE USER, EVENT, TRIGGER, CREATE TABLESPACE
```

开发一般用到的权限
```
create、 update、 insert、  select、  CREATE VIEW、  CREATE ROUTINE、     SHOW VIEW 、CREATE TEMPORARY TABLES、  ALTER
```

权限作用范围:
```
*.*   　  　  ------->所有库的所有表
py.*　  　    ------->py库的所有表
bbs.*　       ------->bbs库的所有表
py.t1　　     ------->py库的t1表
```

设置权限的语句:
```
grant 权限 on 权限作用范围 to 用户 identified by '密码'

给了全部权限，*.*所有作用范围 所有表 app用户使用123密码在10.0.0.1到10.0.0.254IP地址范围内
grant  all privileges   on   *.*   to   app@'10.0.0.%'     identified  by    '123'

将bbs数据库的所有表的create,update,insert,select ,CREATE VIEW权限，给了 IP地址在12网段的用户（bbsuser@'192.168.12.%'），这些用户的密码是‘123’
grant　 create,update,insert,select ,CREATE VIEW　　 on 　　bbs.*　　 to 　　bbsuser@'192.168.12.%' 　　identified by　　 '123';
```


用户组成：
`用户名@‘主机范围’`

主机范围：
```
即IP地址范围，有如下几种写法：
10.0.0.200              -------> 指定就这一个
10.0.0.%                -------> 10.0.0.1--10.0.0.254 范围的ip地址
10.0.0.5%               -------> 10.0.0.50-- 10.0.0.59
%                       -------> 所有的地址都可以
```



```
mysql数据库索引
B树（默认）：
B+tree 
B*tree

+ Hash 索引
哈希索引只有Memory, NDB两种引擎支持，Memory引擎默认支持哈希索引，如果多个hash值相同，出现哈希碰撞，那么索引以链表方式存储，但是，Memory引擎表只对能够适合机器的内存有限的数据集，

要使InnoDB或MyISAM支持哈希索引，可以通过伪哈希索引来实现，叫自适应哈希索引。
主要通过增加一个字段，存储hash值，将hash值建立索引，在插入和更新的时候，建立触发器，自动添加计算后的hash到表里
+ fulltext 全文索引
B树：
cluster indexes 聚集索引 ，随机IO变成顺序IO
辅助索引 ------>人为管控的：unique 普通的 index

+ 前缀索引
根据字段的前N个字符建立索引
```
alter table student add note varchar(200);
alter table student add index idx_note(note(10)); 
```
 
+ 联合索引
多个字段建立一个索引,联合主键是联合索引的特殊形式
```
where a=女生 and b身高=165 and c身材=好
index(a,b,c)

alter table people add index idx(a,b,c);
a,ab,abc,ac 可以走索引或部分走索引(5.6之后 ac 可以走主键索引)
b bc c ca ba 不走索引
原则：把最常用来作为条件查询的列放在前面。

create table people
(
    id int not null auto_increment primary key ,
    name varchar(20),
    gender enum('m','f'),
    shengao int,
    tizhong int
);

alter table people add index idx_gst(gender,shengao,tizhong);
```

+ 主键索引
只能有一个主键。
主键索引:列的内容是唯一值,例如学号.
表创建的时候至少要有一个主键索引，最好和业务无关。

+ 普通索引
加快查询速度，工作中优化数据库的关键。
在合适的列上建立索引，让数据查询更高效。
```
create index index_name on test(name);
alter table test add index index_name(name);
```
在where条件关键字后面的列建立索引才会加快查询速度.
select id,name from test where state=1 order by id group by name;

+ 唯一索引
内容唯一，但不是主键。
```
create unique index index_name on test(name);
```

数据库索引的设计原则
>为了使索引的使用效率更高，在创建索引时，必须考虑在哪些字段上创建索引和创建什么类型的索引

1. 选择唯一性索引


2. 经常需要排序、分组和联合操作的字段建立索引
经常需要ORDER BY、GROUP BY、DISTINCT和UNION等操作的字段，排序操作会浪费很多时间

3. 常作为查询条件的字段建立索引


4. 限制索引的数目
索引的数目不是越多越好。每个索引都需要占用磁盘空间，索引越多，需要的磁盘空间就越大。修改表时，对索引的重构和更新很麻烦。越多的索引，会使更新表变得很浪费时间。

5. 尽量使用数据量少的索引
如果索引的值很长，那么查询的速度会受到影响。例如，对一个CHAR（100）类型的字段进行全文检索需要的时间肯定要比对CHAR（10）类型的字段需要的时间要多

6. 尽量使用前缀来索引
如果索引字段的值很长，最好使用值的前缀来索引。例如，TEXT和BLOG类型的字段，进行全文检索会很浪费时间。如果只检索字段的前面的若干个字符，这样可以提高检索速度。

7. 删除不再使用或者很少使用的索引
表中的数据被大量更新，或者数据的使用方式被改变后，原有的一些索引可能不再需要。数据库管理员应当定期找出这些索引，将它们删除，从而减少索引对更新操作的影响。

8. 小表不应建立索引
包含大量的列并且不需要搜索非空值的时候可以考虑不建索引

### 索引采用BTree、B+Tree
BTree是平衡树，多路搜索树，
+ 开区间
+ 关键字集合分布在整颗树中
+ 任何一个关键字出现且只出现在一个结点中
+ 搜索有可能在非叶子结点命中而结束
+ 搜索有可能在叶子节点命中而结束
+ 其搜索性能等价于在关键字全集内做一次二分查找
+ 自动层次控制
+ 由于限制了除根结点以外的非叶子结点，至少含有M/2个儿子，确保了结点的至少利用率

B+Tree是平衡树，多路搜索树，是BTree的变体
+ 其定义基本与B-树同
+ 所有关键字都出现在叶子结点节点的链表中（稠密索引），且链表中的关键字是有序的
+ 不可能在非叶子结点命中
+ 非叶子结点相当于是叶子结点的索引（稀疏索引），叶子结点相当于是存储（关键字）数据的数据层
+ 更适合文件索引系统


B*Tree
B*Tree 是B+树的变体
```
B\*树定义了非叶子结点关键字个数至少为(2/3)*M，即块的最低使用率为2/3
B*树分配新结点的概率比B+树要低，空间使用率更高
```

```
B+树的分裂：当一个结点满时，分配一个新的结点，并将原结点中1/2的数据
复制到新结点，最后在父结点中增加新结点的指针；B+树的分裂只影响原结点和父
结点，而不会影响兄弟结点，所以它不需要指向兄弟的指针；

B*树的分裂：当一个结点满时，如果它的下一个兄弟结点未满，那么将一部分
数据移到兄弟结点中，再在原结点插入关键字，最后修改父结点中兄弟结点的关键字
（因为兄弟结点的关键字范围改变了）；如果兄弟也满了，则在原结点与兄弟结点之
间增加新结点，并各复制1/3的数据到新结点，最后在父结点增加新结点的指针；
```
### 总结：
二叉搜索树：二叉树，每个结点只存储一个关键字，等于则命中，小于走左结点，大于走右结点；

B（B-）树：多路搜索树，每个结点存储M/2到M个关键字，非叶子结点存储指向关键字范围的子结点；所有关键字在整颗树中出现，且只出现一次，非叶子结点可以命中；

B+树：在B-树基础上，为叶子结点增加链表指针，所有关键字都在叶子结点中出现，非叶子结点作为叶子结点的索引；B+树总是到叶子结点才命中；

B*树：在B+树基础上，为非叶子结点也增加链表指针，将结点的最低利用率从1/2提高到2/3；


AVL Tree：
windows NT内核中应用广泛，适合查找，不适合修改、更新、删除等

红黑树：
+ 广泛用于C++的STL中,map和set都是用红黑树实现的.
+ 著名的linux进程调度Completely Fair Scheduler,用红黑树管理进程控制块,进程的虚拟内存区域都存储在一颗红黑树上,每个虚拟地址区域都对应红黑树的一个节点,左指针指向相邻的地址虚拟存储区域,右指针指向相邻的高地址虚拟地址空间.
+ IO多路复用epoll的实现采用红黑树组织管理sockfd，以支持快速的增删改查.
+ ngnix中,用红黑树管理timer,因为红黑树是有序的,可以很快的得到距离当前最小的定时器.
+ java中TreeMap的实现.

```
```
MySQL事务隔离级别
+ 原子性 Atomicity
+ 一致性 Consistency
+ 隔离性 Isolation
+ 持久性 Durability
ACID

事物的并发问题：
+ 脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据就是脏数据
+ 不可重复读：事务A多次读取同一个数据，事务B在事务B多次读取的过程中，对数据进行了更新并提交，导致事务A多次读取同一数据时，结果不一致
+ 幻读：系统管理员A更改了数据记录的某一个字段值，此时B插入了一条记录，当A修改结束时发现还有一条记录没有修改过来，这就好像发生了幻觉一样，这就是幻读

不可重复读侧重于修改，解决不可重复读只需要锁住满足条件的行。
幻读侧重于新增或删除，解决幻读只需要锁住表


隔离级别：
```
名称                                              脏读    不可重复读     幻读
读未提交（read uncommitted）                      是        是            是
读已提交（不可重复读）（read committed）          否        是            是
可重复读（repeatable read）                       否        否            是
串行化（serializable）                            否        否            否
```


数据库设计范式


乐观锁：


悲观锁：


如何解决事务并发问题





11. mongodb数据库原理
非关系型数据库：高性能，高并发，对数据一致性要去不高，json格式存取
nosql菲关系型数据库总结：
+ nosql不是否定关系数据库，而是作为关系数据库的一个重要补充
+ nosql为了高性能，高并发而生，忽略影响高性能，高并发的功能
+ nosql典型的产品有memcached(纯内存)，redis(持久化缓存)， mongodb(文档型数据库)

BSON文档（对象）是一种计算机数据交换格式，主要被用作MongoDB数据库中的数据存储和网络传输格式，Binary JSON（二进制JSON）
JSON相比，BSON着眼于提高存储和扫描效率

```
BSON文档（对象）由一个有序的元素列表构成。每个元素由一个字段名、一个类型和一个值组成。字段名为字符串。类型包括：
* string
* integer(32 or 64)
* double(64位IEEE 754浮点数)
* decimal128(128位IEEE 754-2008浮点数；Binary Integer Decimal变体)适合作为任意精度为34个十进制数字的数字载体，最大值近似10
* date(整数，uninx时间的毫秒数)
* byte array(二进制数组)
* 布尔(true or false)
* null
* BSON数组
* BSON对象
* JavaScript代码
* md5二进制数据
* 正则表达式
```

BSON的类型名义上是JSON类型的一个超集（JSON没有date或字节数组类型），但是没有像JSON那样的通用“数字”（number）类型

12. redis原理
redis特点：
* 高性能高并发
* 数据持久化功能
* 支持多数据类型，主从复制和集群
* 管理不再使用SQL

13. web安全


14. 用户行为分析，BI


15. 深度学习CNN/RNN/GAN网络结构


16. numpy,scipy,pandas,matplotlib


17. flask, tornado, django


18. restful api


19. 
os.listdir(path)
os.walk(path)
os.walk(top[, topdown=True[, onerror=None[, followlinks=False]]])
方法参数说明：
top：要遍历的目录的路径
topdown：可选，如果为 True，则优先遍历 top 目录，以及 top 目录下的每一个子目录，否则优先遍历 top 的子目录，默认为 True
onerror: 可选， 需要一个 callable 对象，当 walk 异常时调用
followlinks：可选， 如果为 True，则会遍历目录下的快捷方式(linux 下是 symbolic link)实际所指的目录，默认为 False
args：包含那些没有 '-' 或 '--' 的参数列表

返回值: 三元组 (root, dirs, files)
root ：所指的是当前正在遍历的目录的地址
dirs ：当前文件夹中所有目录名字的 list (不包括子目录)
files ：当前文件夹中所有的文件 (不包括子目录中的文件)
def work_dir(file_dir):
    print'\n\n<><><><><> work dir <><><><><>'
    for root, dirs, files in os.walk(file_dir):
        print'\n========================================'
        print "root : {0}".format(root)
        print "dirs : {0}".format(dirs)
        print "files : {0}".format(files)
​
        for file in files:
            try:
                print'-----------------------------------'
                
                file_name = os.path.splitext(file)[0]
                file_suffix = os.path.splitext(file)[1]
                file_path = os.path.join(root, file)
                file_abs_path = os.path.abspath(file)
                file_parent = os.path.dirname(file_path)
​
                print "file : {0}".format(file)
                print "file_name : {0}".format(file_name)
                print "file_suffix : {0}".format(file_suffix)
                print "file_path : {0}".format(file_path)
                print "file_abs_path : {0}".format(file_abs_path)
                print "file_parent : {0}".format(file_parent)
                
            except Exception, e:
                print "Exception", e



os.path.splitext()：分离文件名和扩展名

file = "file_test.txt"
file_name = os.path.splitext(file)[0] # 输出：file_test
file_suffix = os.path.splitext(file)[1] # 输出：.txt

os.path.exists()：判断文件或目录是否存在
os.path.isfile()：判断是否是文件
os.path.isdir()：判断是否是目录
os.path.dirname()：获取当前文件所在的目录，即父目录
os.makedirs()：创建多级目录
os.mkdir()：创建单级目录
os.path.getsize()：获取文件大小

20. 
格式化符号
```
%y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12）
%M 分钟数（00=59）
%S 秒（00-59）
%a本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X本地相应的时间表示
%Z 当前时区的名称
%% %号本身
```

21.
```
map()函数：
map() 会根据提供的函数对指定序列做映射。
第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。
```
map() 函数语法：
map(function, iterable, ...)

function – 函数
iterable – 一个或多个序列
实例：

>>> map(lambda x: x ** 2, [1, 2, 3, 4, 5])  # 使用 lambda 匿名函数
[1, 4, 9, 16, 25]
 
# 提供了两个列表，对相同位置的列表数据进行相加
>>> map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
[3, 7, 11, 15, 19]

zip()函数：

zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。
如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

zip 语法：

zip([iterable, ...])
1
iterabl – 一个或多个迭代器;

实例：

>>>a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 打包为元组的列表
[(1, 4), (2, 5), (3, 6)]
>>> zip(a,c)              # 元素个数与最短的列表一致
[(1, 4), (2, 5), (3, 6)]
>>> zip(*zipped)          # 与 zip 相反，*zipped 可理解为解压，返回二维矩阵式
[(1, 2, 3), (4, 5, 6)]

在二维矩阵变换（矩阵的行列互换）这样一个操作中，用到了以上两个函数：

>>> a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> zip(*a)
[(1, 4, 7), (2, 5, 8), (3, 6, 9)]
>>> map(list,zip(*a))
[[1, 4, 7], [2, 5, 8], [3, 6, 9]]

```
