#### vtmysql5devp2
#####Manipulating data
######basics
######warnings
######changing syntax inter
```
set sql_mode=ansi
[see here to check sql_mode][https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwiLm8KBvcjLAhWqlIMKHVlnDjsQFggdMAA&url=http%3A%2F%2Fdev.mysql.com%2Fdoc%2Fen%2Fsql-mode.html&usg=AFQjCNH9tpAIuRZz737R7FV0xrh7Wd4j0g&sig2=kaywR6VXnuaevNuiuN4K5Q)



















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
