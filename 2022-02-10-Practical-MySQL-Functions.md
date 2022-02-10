---
layout:     post
title:      Practical MySQL Functions
subtitle:   RiceQuant
date:       2022-02-10
author:     JieKun Liu
header-img: img/the-first.png
catalog:   true
tags:
    - MySQL
---

MySQL

- Numeric Functions

  - -- select ROUND(5.7345,3)
    -- select TRUNCATE(5.7345,1)
    -- select ceiling(5.2)
    -- select floor(4.9)
    -- select abs(-2.2)
    -- select rand(0.9)

- String FUnctions

  - -- select length('sky')
    -- select upper('sky')
    -- select lower('sky')
    -- select ltrim('    sky')
    -- select rtrim('    sky    ')
    -- select trim('    sky    ')
    -- select left('kindergarten',4)
    -- select right('dbsabs',4)

  - -- select substring('kindergarten',3,5)
    -- select locate('n','kindergarten')
    -- select replace('kindergarten','garten','garden')
    -- select concat('first','last')
    /*use sql_store;
    select concat(first_name,' ',last_name) as full_name

    from customers*/

- DateFunctions

  - -- select now(),curdate(),curtime()
    -- select year(now())
    -- select day(now())
    -- select hour(now())
    -- select dayname(now())
    -- select monthname(now())
    -- select extract(hour from now())

- Formatting Date and Times

  - -- select date_format(now(),'%M %D %Y')
    -- select time_format(now(),'%H:%i %p')

- Calculating Dates and Times

  - -- select now(),date_add(now(),interval -1 year),date_sub(now(),interval 1 year)
    -- select datediff('2022-02-02','2022-01-09')
    -- select time_to_sec('9:00')-time_to_sec('8:59')

- The IFNULL and COALESCE Functions

  - /*select 
    	order_id,
    	ifnull(shipper_id,'not assigned') as shipper
            
    from orders

    use sql_store;
    select 
    	order_id,
        ifnull(shipper_id,'...'),
    	coalesce(shipper_id,comments,'not assigned') as shipper
            
    from orders
    */

- The IF Function

  - select 
    	product_id,
        name,
        orders,
        if(orders=1,'Once','Many times') as frequency
    from
    (
    SELECT
    product_id,
    name,
    count(product_id) as orders

    FROM order_items oi
    left join products p using(product_id)
    group by product_id
    ) as summary 

- The CASE Operator

  - select 
    	order_id,
        CASE
    		WHEN YEAR(order_date)=YEAR(now()) THEN 'Active'
    		WHEN YEAR(order_date)=YEAR(now())-1 THEN 'Last Year'
    		WHEN YEAR(order_date)<YEAR(now())-1 THEN 'Archived'
    		ELSE 'Future'
    	END as category
    from orders

