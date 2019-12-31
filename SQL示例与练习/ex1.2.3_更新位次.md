# 1.2.3 更新位次

## 问题:
**准备数据:**
```sql
create table district_products_2(
	district text not null,
    name text not null,
    price numeric(10, 3) not null,
    ranking int
);
insert into district_products_2(
	district,
    name,
    price
) values ('东北', '橘子', 100),
		('东北', '苹果', 50),
		('东北', '葡萄', 50),
		('东北', '柠檬', 30),
		('关东', '柠檬', 100),
		('关东', '菠萝', 100),
		('关东', '苹果', 100),
		('关东', '葡萄', 70),
		('关西', '柠檬', 70),
		('关西', '西瓜', 30),
		('关西', '苹果', 20);
```

**问题:**
如下更新ranking列:
```textmate
 district | name |  price  | ranking
----------+------+---------+---------
 东北     | 橘子 | 100.000 |       1
 东北     | 苹果 |  50.000 |       2
 东北     | 葡萄 |  50.000 |       2
 东北     | 柠檬 |  30.000 |       4
 关东     | 柠檬 | 100.000 |       1
 关东     | 菠萝 | 100.000 |       1
 关东     | 苹果 | 100.000 |       1
 关东     | 葡萄 |  70.000 |       4
 关西     | 柠檬 |  70.000 |       1
 关西     | 西瓜 |  30.000 |       2
 关西     | 苹果 |  20.000 |       3
```
## 答案:
**使用连接子查询:**
```sql
update district_products_2 as d1
    set ranking = (select count(*) + 1
                    from district_products_2 as d2
                    where d2.district = d1.district
                        and d2.price > d1.price);
```

**使用rank函数:**

🤔
