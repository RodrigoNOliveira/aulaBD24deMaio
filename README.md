SELECT * FROM LOJA.offices;

SELECT customername from customers where customerNumber not in (SELECT customerNumber from orders where orderDate >"2005-04-01") and state='CA';

SELECT customername from customers where creditLimit < any (SELECT creditLimit from customers);

SELECT nome from TB_FUNCIONARIOS where salario > all(SELECT salario from TB_FUNCIONARIOS,TB_CARGOS where TB_CARGOS .ID=TB_FUNCIONARIOS.CARGO_ID AND TB_CARGOS.CARGO="PROGRAMADOR") ORDER BY nome;


SELECT customername from customers c where EXISTS(SELECT customerNumber from orders where customerNumber=c.customerNumber and orderDate ="2005-05-30");

SELECT cliente.* FROM (SELECT salesRepEmployeeNumber,customerName,PHONE FROM customers) AS cliente JOIN (SELECT employeeNumber from employees where jobtitle like '%rep%') AS emp ON cliente.salesRepEmployeeNumber = emp.employeeNumber order by cliente.customerName;


SELECT CITY, COUNTRY, PHONE FROM customers WHERE CUSTOMERNUMBER = (SELECT CUSTOMERNUMBER FROM customers WHERE STATE ='NV');


SELECT PRODUCTVENDOR, SUM(QUANTITYINSTOCK) FROM products GROUP BY PRODUCTVENDOR HAVING SUM(quantityInStock) > (SELECT SUM(QUANTITYINSTOCK) AS SOMA FROM products GROUP BY productVendor ORDER BY SOMA LIMIT 1 OFFSET 3) ORDER BY productVendor;



Select firstName, lastname from employees where employeeNumber in (Select salesRepEmployeeNumber from customers, payments where customers.customerNumber = payments.customerNumber and paymentDate < '2004-12-06' and country ='USA');


select productName from products where productCode in (select productCode from orderdetails where quantityOrdered < any (select quantityOrdered from orderdetails));

select orders.* from orders where orderNumber in (select orderNumber from orderdetails where priceEach < '50.00');
