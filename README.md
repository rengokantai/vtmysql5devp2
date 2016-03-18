#### vtmysql5devp2


#####configuration
######startup
```
mysqld --verbose --help
```


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

#####inserting data
######demonstrations
ternary operator, and get date of 25 years ago.
```
CONCAT('San' , IF(MOD(DAY(CURDATE()),2),'Joe','Meo')),CURDATE()-INTERVAL 25 YEAR
```
















#####Trigger
######use of trigger.
for data validation:  
######syntax
timing: before, after  
op: insert update delete

######exam
```sql
create trigger trigname before insert on tbname
for each row
set new.cls2 = month(new.cls3)
```

delete table1 and copy to table2:
```sql
create trigger tgname after delete on table1
for each row
insert into table2 values(OLD.clname1,OLD.clname2);
```

######explor
```
show create trigger tgname\G
```

######trigger metadata
```
show triggers where `Trigger` = 'tgname'\G
desc information_schema.triggers;
```
###### drop trigger

trn (per trigger) and trg (per table) file  
trn file is short(placeholder), trg file is long  

trigger name may diff in database, not table!
```
drop triggger tgname;
```

######limitations
cannot return a result set to client.  
cannot manipulate rows in table used by statement that launched it.  
changes to columns in current row must be performed in a BEFORE trigger














#####indexes
######Index basics
index is a seperate table maintains row order for a column or comb of columns of a table  
issues: slows data manipulation operation because it is dynamically maintained(addition storage)

######defining indexes for table
```
show index from tbname\G
```


###### add indexes
```
alter table tbname add primary key(clname)
alter table tbname add index(clname)
alter table tbname add index idxname (clname)
create index idxname on tbname(clname)
drop index idxname on tbname
```
###### dropping indexes
```
drop index idxname on tbname
alter table tbname drop index a, drop index b
```
######compound indexes
```sql
create table tbname(
firstname varchar(10),
lstaname varchar(20),
.....,
index fullname(firstname,lastname)
);
```
######prefix

only index first n chars.
```sql
create table country(
name char(200),
...,
index (name(10))
```

note sub_part

######fulltext index
```sql
create table tbname(
clname varchar(100),
FULLTEXT KEY keyname(clname)
)
```

```
select * from tbname where match (clname) against ('keywordxxxx');
```

search  text contains keyword1 OR keyword2
```
select * from tbname where match (clname) against ('keyword1 keyword2');
```
score means how similiar
```
select match(clname) against ('a b') Score , clname from tbname where match(clname) against('a b');
```

add + sign means mandatory  (keyword1 is mandatory)
```
select * from tbname where match (clname) against ('+keyword1 keyword2' IN BOOLEAN MODE);
```

add - sign means sentence with k2 can not have k1.
```
select * from tbname where match (clname) against ('-keyword1 keyword2' IN BOOLEAN MODE);
```
ywith query expansion
```
select * from tbname where match (clname) against ('keyword2' WITH QUERY EXPANSION);
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
