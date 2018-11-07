# Web-Vulnerability-Scanner
Web Vulnerability Scanner: SQL
### 目的：熟悉SQL漏洞等常见Web漏洞原理，重点不在效率和使用，如果正八经儿检测，sqlmapapi甚至是各种工具就方便快捷
## 实现功能
1. 针对SQL注入漏洞、SQL盲注、~~XSS注入~~
2. 通过匹配报错出来的信息，可以正则判断出所用的数据库

## SQL注入总结（根据sqlmap）
## 注入类型
## 1. First order Injection，一级注入
### > 发生在应用与用户交互的地方
### - 注入位置有：
  - GET,POST型的，表单的post提交和一些按钮的POST提交，sqlmap默认注入等级
  - HTTP报文的头部字段，包括Cookie/User-Agent等，也可能发生SQL注入。sqlmap等级2会检测Cookie，等级3会测试 User-Agent、Referer
### - 参数属性类型：
  - 整形（整形参数之后跟的语句不必打破变量区）
  - 字符型
### 2. Second order Injection，二级注入
> 数据库和应用之间。通常网站开发者可能会十分注意与用户发生交互的地方，这些地方就很少会有SQL注入漏洞了。而开发对与从数据库查询出来的信息可能十分信任，而这就是攻击者的机会所在——即便从数据库查询出来的数据也不是可靠的。攻击者构造一个带有SQL语句的用户帐号，成功注册并登录后，网页session会话使用的用户名是从数据库查询出来的，之后用户发布帖子，数据库执行了插入语句，而且参数带有该用户名，开发十分信任这个变量，在这里偷懒了，可能就发生了SQL注入。

## 注入方式
## 1. B: Boolean-based blind SQL injection（布尔型注入）<br>
### `Title: AND boolean-based blind - WHERE or HAVING clause`<br>
### `Payload: user=user1' AND 4676=4676 AND 'ZzOn'='ZzOn`
## 2. E: Error-based SQL injection（报错型注入）<br>
###  ` Title: MySQL >= 5.5 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (BIGINT UNSIGNED)`<br>
###  `Payload: user=user1' AND (SELECT 2*(IF((SELECT * FROM (SELECT CONCAT(0x716b786b71,(SELECT (ELT(7994=7994,1))),0x717a787871,0x78))s), 8446744073709551610, 8446744073709551610))) AND 'XSuv'='XSuv`
## 3. U: UNION query SQL injection（可联合查询注入）<br>
###  `Title: Generic UNION query (NULL) - 2 columns`<br>
###  `Payload: user=user1' UNION ALL SELECT CONCAT(0x716b786b71,0x6a6a6668724d514d5448686874774f486d634550735659727866554e65554e4e4f55504146706471,0x717a787871),NULL-- QvWZ`
## 4. S: Stacked queries SQL injection（可多语句查询注入）
## 5. T: Time-based blind SQL injection（基于时间延迟注入）<br>
###  `Title: MySQL >= 5.0.12 AND time-based blind`<br>
###  `Payload: user=user1' AND SLEEP(5) AND 'EJXX'='EJXX`
## 6. Q: inline_query(内联查询)

    
## SQL漏洞扫描代码实现
## ![avatar](http://drops.xmd5.com/full/633282f29a309bdd23eed56248fc943a6f97aaa5.jpg)
### 1. 判断注入位置：
  - 判断GET,POST方法
  - HTTP报文的头部字段——>设置Cookie、User-Agent、Referer
### 2. 前缀PREFIXES
### 2. 后缀SUFFIXES
### 3. 参数 
