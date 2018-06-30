# MySQL 函数

## 数学函数

> 数学函数主要用来处理数值数据.在有错误产生时,数学函数将会返回空值.

### 绝对值函数 abs() 和返回圆周率的函数 PI()

**abs(x)返回 x 的绝对值**

**pi()返回圆周率的值.**默认的显示小数位数是6位.

### 平方根函数 sqrt(x)和求余函数 mod(x,y)

**sqrt(x)**返回非负数的二次平方根.负数没有平方根,因此sqrt(-49)返回的结果为**null**.

```mysql
sqrt(9)  -> 3   
sqrt(-49)  -> null
```

**mod(x,y)**返回 x 被 y 除后的余数,对于带有小数部分的数值也起作用.,返回除法运算后的精确余数.

```mysql
mod(31,8) -> 7
mod(45.6,6) -> 3.6
```

### 获取整数的函数 ceil(x) ceiling(x) floor(x)

**ceil(x)**和**ceiling(x)**意义相同,返回不小于 x 的最小整数.返回值转化为一个`bigint`

```mysql
ceil(-3.35)  -> -3
ceiling(3.5) -> 4
```

**floor( x)**返回不大于 x 的最大整数值,返回值转化为一个 `bigint`

```mysql
floor(-3.35) -> -4
floor(3.34) -> 3
```

### 获取随机数的函数 rand()和 rand(x)

**rand(x)** 返回一个随机浮点值 v, 范围在0~1之间

不带参数的 **rand()**每次产生的随机数值是不同的.

带参数的 rand(x)的参数相同时,将产生相同的随机数,不同的 x 产生的随机数值不同.

### 函数 round(x), round(x,y) 和 truncate(x,y)

**round(x)**返回最接近于参数x 的整数,对 x 值进行四舍五入.

```mysql
round(-1.14)  ->  -1
round(-1.67)  -> -2
round(1.1)  -> 1
```

**round(x,y)**返回最接近于参数 x 的数,其值保留到小数点后面 y 位,,若 y 为负值,则将保留 x 值到小数点左边 y 位.

```mysql
round(1.38,1) -> 1.4
round(232.38,-1) -> 230
round(232.38,2) -> 200
```

**truncate(x,y)**返回被舍弃至小数点后 y 位的数字 x.若 y 的值为0,则结果不带有小数点.若 y 为负数,则截去 x 小数点左起第 y 位开始后面所有低位的值.

```mysql
truncate(1.99,1)  -> 1.9
truncate(19.99, -1) -> 10
```

### 符号函数 sign(x)

**sign(x)**返回参数的符号, x 的值为负,零或正时,返回的结果依次为-1,0,1

----

## 字符串函数

> 字符串函数主要用来处理数据库中的字符串数据.

### 计算字符串字符数的函数和字符串长度的函数

**char_length(str)**返回值为字符串 str 包含的字符个数,一个多字节字符算作一个单字符.

**length(str)**返回值为字符串的字节长度.

英文字符的个数和所占的字节数相同,一个字符占一个字节.

### 合并字符串函数 concat(s1,s2,...), concat_ws(x,s1,s2,...)

**concat(s1,s2,...)**返回结果为连接参数产生的字符串,,如有任何一个参数为 null, 返回结果为 null.如果变量中任有一个二进制字符串,则结果为一个二进制字符串.

**concat_ws(x,s1,s2...)**将字符串用分隔符连接起来. x 为分隔符,如果分隔符为 null, 则结果为 null,.函数会忽略掉任何分隔符参数后的 null 值.

### 替换字符串的函数 insert(s1,x,len,s2)

**insert(s1,x,len,s2)**返回字符串s1,其子字符串起始于 x 位置和被字符串 s2取代的 len 字符.

```mysql
select insert('quest',2,4,'what') as col1,insert('quest',-1,4,'what') as col2,insert('quest222222',3,100,'what') as col3;
+-------+-------+--------+
| col1  | col2  | col3   |
+-------+-------+--------+
| qwhat | quest | quwhat |
+-------+-------+--------+
```

如果 len 的长度大于其他字符串,将从位置 x 开始替换.如果x 超出了字符串长度,则返回原字符串.

### 字符大小写转换函数

**lower(str)**或者**lcase(str)**可以将字符串 str 中的字符字符全都转换成小写字母.

 **upper(str)**或者**ucase(str)**可以将字符串 str 中的字母字符全部转换成大写字母.



### 获取指定长度的字符串的函数 left( s,n)和 right( s,n)

**left(s,n)**返回字符串 s 开始的最左边 n 个字符.

**right(s,n)**返回字符串中最右边 n 个字符.



### 填充字符串的函数 Lpad(s1,len,s2)和 rpad(s1,len,s2)

**Lpad(s1,len,s2)**返回字符串 s1,其左边由字符串s2填补到 len 字符长度,假如 s1的长度大于 len. 则返回值缩短至 len 字符.

```mysql
select lpad('hello',4,'?') as col1, lpad('hello',10,'?') as col2;
+------+------------+
| col1 | col2       |
+------+------------+
| hell | ?????hello |
+------+------------+
```

**Rpad(s1,len,s2)**返回字符串s1,其右边被字符串 s2填补值 len 字符长度.假如字符串 s1

的长度大于 len, 则返回值被缩短到 len 字符长度.

```mysql
select rpad('hello',4,'?') as col1, rpad('hello',10,'?') as col2;
+------+------------+
| col1 | col2       |
+------+------------+
| hell | hello????? |
+------+------------+
```

### 删除空格的函数 Ltrim(s), rtrim(s)和 trim(s)

**Ltrim(s)**返回字符串 s, 字符串左侧空格字符被删除.

**rtrim(s)**返回字符串s,字符串右侧空格字符被删除.

**trim(s)**删除字符串 s 两侧的空格.

### 删除指定字符串的函数 trim(s1 from s)

**trim(s1 from s)**删除字符串 s 中两端所有的子字符串s1.

### 重复生成字符串的函数 repeat(s,n)

**repeat(s,n)**返回一个由重复的字符串 s 组成的字符串,字符串s 的数目等于 n. 若 n<=0,则返回一个空字符串.若 s 或 n 为 null, 则返回 null.

### 获取子串的函数 substring(s,n,len)

从字符串 s 返回一个长度同 len 字符相同的子字符串,,起始于位置 n. 如果没有 len 参数,则返回从 n 开始到结尾的字符串.

### 字符串逆序的函数 reverse(s)

**reverse(s)**将字符串 s 反转,返回的字符串顺序和原来得相反.

---

## 日期和时间函数

### 获取当前日期的函数和获取当前时间的函数.

**curdate()**和**current_date()**函数作用相同,将当前日期按照'yyyy-mm-dd'或者 YYYYMMDD 格式的值返回.

**curtime()**和**current_time()**函数作用相同.将当前时间以' HH:MM:SS'或 hhmmss的格式返回.

### 获取当前日期和时间的函数

`current_timestamp()`,`localtime()`,`now()`,`sysdate()`4个函数作用相同,均返回当前日期和时间值.

格式为"YYYY-MM-DD HH:MM:SS"或者 YYYYMMDDHHMISS.

### 获取月份的函数 month(date) 和 monthname(date)

**month(date)**返回 date 对应的月份,范围在 1~12.

**monthname(date)**返回日期 date 对应月份的英文名.

### 获取星期的函数 dayname(d) , dayofweek(d), weekday(d)

**dayname(d)**:返回 d 对应的工作日的英文名称.

**dayofweek(d)**: 返回 d 对应的一周中的索引. 1 表示周日, 2表示周一....

**weekday(d)**:返回 d 对应的工作日索引. 0表示周一,1表示周二....

### 获得星期数的函数 week(d)和 weekofyear(d)

**week(d)**计算日期 d 是一年中的第几周.

**weekofyear(d)**计算某天位于一年中的第几周.

### 获取天数的函数 dayofyear(d)和 dayofmonth(D)

**dayofyear(d)**返回 d 是一年中的第几天,范围是1~366.

**dayofmonth(d)**返回指定日期在一个月中的位置.

