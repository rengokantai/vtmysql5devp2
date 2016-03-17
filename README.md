#### vtmysql5devp2
#####Manipulating data
######basics
######warnings
######changing syntax inter
```
set sql_mode=ansi_quotes(not allow double quote as column name) ,pipes_as_concat,....
```
[see here to check sql_mode](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwiLm8KBvcjLAhWqlIMKHVlnDjsQFggdMAA&url=http%3A%2F%2Fdev.mysql.com%2Fdoc%2Fen%2Fsql-mode.html&usg=AFQjCNH9tpAIuRZz737R7FV0xrh7Wd4j0g&sig2=kaywR6VXnuaevNuiuN4K5Q)

restore:
```
set sql_mode='';
```
######warning to errors
```
mysql -u root --show-warnings
```
Or: (tinyint only support 2-digit number)
```
insert into tbname values(1),(12),(123);
show warnings\G
```
```
set sql_mode=traditional  //warning=error!
```
######interpre error message
error code:  
server error: <2000  
client error >=2000  
######note warnings
```
set sql_notes = 0
```
note warnings will no longer be returned.
######system error warn
(HY000) file system error code
````
select * from tbname into outfile 'c:/txt';
```

get error code
```
perror (0,1,2,...)
```
Or (must in unix)
```
mysql> system perror 2  (or  \! perror 2)
```

















#####efficiency check
######
procedure analyse keyword: s,not z
```
select * from yd procedure analyse()\G
```
######explain
indexed column vs non-indexed column:  
```
explain select * from test;
```
note the following : type (const vs all), row(1 vs 100000..), key(primary vs null)
