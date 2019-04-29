# Loan
Loan

1. Write a query to display category and number of items in that category. Give the count an alias name of Count_category.
Display the details on the sorted order of count in descending order.

A) SELECT item_category,count(item_id) Count_category FROM
   item_master GROUP BY item_category ORDER BY Count_category DESC;

------------------------------------------------------------------------------------------------------------------------------------------

2. Write a query to display the number of employees in HR department. Give the alias name as No_of_Employees.

A) SELECT count(employee_id) No_of_Employees FROM 
   employee_master WHERE department='HR';
   
 -----------------------------------------------------------------------------------------------------------------------------------------
 
 3. Write a query to display employee id, employee name, designation and department for employees who have never been issued an
 item as a loan from the company. Display the records sorted in ascending order based on employee id.

A) SELECT employee_id,employee_name,designation,department FROM  employee_master 
   WHERE employee_id NOT IN (SELECT employee_id FROM employee_issue_details)
   ORDER BY employee_id;
   
------------------------------------------------------------------------------------------------------------------------------------------

4. Write a query to display the employee id, employee name who was issued an item of highest valuation. 
In case of multiple records, display the records sorted in ascending order based on employee id.[Hint Suppose an item called dinning
table is of 22000 and that is the highest price of the item that has been issued. So display the employee id and employee name who
issued dinning table whose price is 22000.]

A) SELECT employee_id,employee_name FROM employee_master
   WHERE employee_id IN(SELECT employee_id FROM employee_issue_details
   WHERE item_id IN (SELECT item_id FROM item_master
   WHERE item_valuation=(SELECT max(item_valuation) FROM 
   item_master i JOIN employee_issue_details e ON i.item_id=e.item_id)));
   
 -------------------------------------------------------------------------------------------------------------------------------------
 
 5. Write a query to display issue_id, employee_id, employee_name. Display the records sorted in ascending order based on issue id.

A) SELECT eid.issue_id, eid.employee_id, em.employee_name
   FROM employee_master em JOIN  employee_issue_details eid
   ON em.employee_id=eid.employee_id ORDER BY eid.issue_id;
   
 ------------------------------------------------------------------------------------------------------------------------------------
 
 6. Write a query to display employee id, employee name who don’t have loan cards.Display the records sorted in ascending order 
 based on employee id.

A) SELECT employee_id,employee_name FROM employee_master
   WHERE employee_id NOT IN(SELECT employee_id FROM employee_card_details);
   
  ----------------------------------------------------------------------------------------------------------------------------------
  
 7. Write a query to count the number of cards issued to an employee “Ram”.  Give the count an alias name as No_of_Cards.

A) SELECT count(loan_id) No_of_Cards FROM
   employee_card_details WHERE employee_id IN 
   (SELECT employee_id FROM employee_master WHERE employee_name='Ram');
                             (or)
    SELECT count(loan_id) No_of_Cards FROM  
    employee_card_details c JOIN  employee_master e
     ON c.employee_id = e.employee_id
    WHERE e.employee_name= 'Ram';
    
 --------------------------------------------------------------------------------------------------------------------------------------
 
 8. Write a query to display the count of customers who have gone for loan type stationary. Give the count an alias name 
 as Count_stationary.

A) SELECT count(e.employee_id) Count_Stationary
   FROM employee_card_details e JOIN loan_card_master l
   ON e.loan_id=l.loan_id WHERE l.loan_type='Stationary';
   
 ----------------------------------------------------------------------------------------------------------------------------------
 
 9. Write a query to display the employee id, employee name   and number of items issued to them. Give the number of items
 an alias name as Count. Display the details in descending order of count and then employee_id
 
A) SELECT e.employee_id,employee_name,count(e.item_id) Count FROM 
   employee_issue_details e JOIN employee_master em ON e.employee_id=em.employee_id
   GROUP BY e.employee_id ORDER BY count DESC,e.employee_id;
   
  ------------------------------------------------------------------------------------------------------------------------------------
  
  10. Write a query to display the employee id, employee name who was issued an item of minimum valuation.In case of multiple records,
  display them sorted in ascending order based on employee id.[Hint Suppose an item called pen is of rupees 20 and that is the 
  lowest price. So display the employee id and employee name who issued pen where the valuation is 20.]
  
A)  SELECT employee_id,employee_name FROM employee_master
    WHERE employee_id IN(SELECT employee_id FROM employee_issue_details
    WHERE item_id IN (SELECT item_id FROM item_master
    WHERE item_valuation=(SELECT min(item_valuation) FROM 
    item_master i JOIN employee_issue_details e ON i.item_id=e.item_id)))
    ORDER BY employee_id;
    
  --------------------------------------------------------------------------------------------------------------------------------------
  
  11. Write a query to display the employee id, employee name and total valuation of the product issued to each employee. 
  Give the alias name as TOTAL_VALUATION.Display the records sorted in ascending order based on employee id.Consider only
  employees who have been issued atleast 1 item.

A) SELECT e.employee_id,em.employee_name,sum(i.item_valuation) TOTAL_VALUATION FROM
   item_master i JOIN employee_issue_details e ON e.item_id=i.item_id
   JOIN employee_master em ON em.employee_id=e.employee_id
   GROUP BY e.employee_id ORDER BY employee_id;
   
------------------------------------------------------------------------------------------------------------------------------------------

12. Write a query to display distinct employee id, employee name who kept the item issued for more than a year. 
Hint: Use Date time function to calculate the difference between item issue and return date. Display the records only
if it is more than 365 Days.Display the records sorted in ascending order based on employee id.

A) SELECT DISTINCT e.employee_id,e.employee_name FROM 
   employee_master e JOIN  employee_issue_details ei ON e.employee_id=ei.employee_id
   WHERE datediff(ei.return_date,ei.issue_date)>365
   ORDER BY employee_id;
   
----------------------------------------------------------------------------------------------------------------------------------------

13. Write a query to display employee id, employee name and count of items of those who asked for more than 1 furniture.
Give the alias name for count of items as COUNT_ITEMS.Display the records sorted in ascending order on employee id.

A) SELECT e.employee_id,e.employee_name,count(ei.item_id) COUNT_ITEMS FROM
   employee_master e JOIN employee_issue_details ei ON e.employee_id=ei.employee_id
   JOIN item_master i ON ei.item_id=i.item_id
   WHERE i.item_category='Furniture' 
   GROUP BY ei.employee_id HAVING count(ei.item_id)>1;
   
------------------------------------------------------------------------------------------------------------------------------

14. Write a query to display the number of men & women Employees.
The query should display the gender and number of Employees as No_of_Employees. 
Display the records sorted in ascending order based on gender.

A) SELECT gender,count(employee_id) FROM employee_master
   GROUP BY gender ORDER BY gender;
   
 ----------------------------------------------------------------------------------------------------------------------------------
 
 15. Write a query to display employee id, employee name who joined the company after 2005.
 Display the records sorted in ascending order based on employee id.

A) SELECT employee_id,employee_name FROM employee_master
   WHERE year(date_of_joining)>'2005'
   ORDER BY employee_id;
   
-----------------------------------------------------------------------------------------------------------------------------------------

16. Write a query to get the number of items of the furniture category issued and not issued. 
The query should display issue status and the number of furniture as No_of_Furnitures.Display 
the records sorted in ascending order based on issue_status.

A) SELECT issue_status,count(item_id) No_of_Furniture FROM
   item_master WHERE item_category='Furniture'
   GROUP BY issue_status ORDER BY issue_status;
   
 --------------------------------------------------------------------------------------------------------------------------------
 
 17. Write a query to find the number of items in each category, make and description. 
 The Query should display Item Category, Make, description and the number of items as No_of_Items.
 Display the records in ascending order based on Item Category, then by item make and then by item description.

A) SELECT item_category,item_make,item_description,count(item_id) No_of_items FROM
    item_master GROUP BY item_category,item_make,item_description 
    ORDER BY item_category,item_make,item_description;
    
-------------------------------------------------------------------------------------------------------------

18. Write a query to display employee id, employee name, item id and item description of employees who were issued item(s)
in the month of January 2013. Display the records sorted in order based on employee id and then by item id in ascending order.

A) SELECT e.employee_id,employee_name,i.item_id,i.item_description FROM
   employee_master e JOIN employee_issue_details ei ON e.employee_id=ei.employee_id
   JOIN item_master i ON i.item_id=ei.item_id
  WHERE month(ei.issue_date)='01' and year(ei.issue_date)='2013'
   ORDER BY employee_id,item_id;
   
 --------------------------------------------------------------------------------------------------------------------------------
 
 19. Write a query to display the employee id, employee name and count of item category of the employees 
 who have been issued items in at least 2 different categories.Give the alias name for category count as COUNT_CATEGORY.
 Display the records sorted in ascending order based on employee id.

A) SELECT ei.employee_id,e.employee_name,count(DISTINCT i.item_category) COUNT_CATEGORY FROM
   employee_master e JOIN employee_issue_details ei ON e.employee_id=ei.employee_id
   JOIN item_master i ON i.item_id=ei.item_id
    GROUP BY ei.employee_id
    HAVING COUNT_CATEGORY>=2
    ORDER BY employee_id;
    
--------------------------------------------------------------------------------------------------------------------------------

20. Write a query to display the item id , item description which was never issued to any employee. 
Display the records sorted in ascending order based on item id.

A) SELECT item_id, item_description FROM item_master  
   WHERE item_id NOT IN (SELECT item_id from employee_issue_details)
   ORDER BY item_id;
   
 ----------------------------------------------------------------------------------------------------------------------------------
 21. Write a query to display the employee id, employee name andtotal valuationfor the employees who has issued minimum total
 valuation of the product.  Give the alias name for total valuation as TOTAL_VALUATION.[Hint: Suppose an employee E00019 
 issued item of price 5000, 10000, 12000 and E00020 issue item of price 2000, 7000 and 1000. 
 So the valuation of items taken by E00019 is 27000 and for E00020 it is 10000. So the employee id, employee name of E00020 
 should be displayed. ]

A) SELECT e.employee_id,em.employee_name,sum(i.item_valuation) TOTAL_VALUATION FROM
    item_master i JOIN employee_issue_details e ON e.item_id=i.item_id
    JOIN employee_master em ON em.employee_id=e.employee_id
    GROUP BY e.employee_id HAVING sum(i.item_valuation)<=ALL(
   SELECT sum(i.item_valuation) TOTAL_VALUATION FROM
   item_master i JOIN employee_issue_details e ON e.item_id=i.item_id
   JOIN employee_master em ON em.employee_id=e.employee_id
   GROUP BY e.employee_id);
   
 ------------------------------------------------------------------------------------------------------------
 
 22. Write a query to display the employee id, employee name, card issue date and card valid date.Order by employee name 
 and then by card valid date. Give the alias name to display the card valid date as CARD_VALID_DATE.[Hint:  Validity in years
 for the loan card is given in loan_card_master table. Validity date is calculated by adding number of years in the loan card issue
 date. If the duration of year is zero then display AS 'No Validity Date'. ]

A) SELECT e.employee_id,e.employee_name,card_issue_date,
   case
when l.duration_in_years>0 then date_add(ec.card_issue_date,interval l.duration_in_years year)
when l.duration_in_years=0 then 'No Validity Date' end CARD_VALID_DATE 
FROM 
employee_master e JOIN employee_card_details ec ON e.employee_id=ec.employee_id
JOIN loan_card_master l ON l.loan_id=ec.loan_id
ORDER BY employee_name,CARD_VALID_DATE;

---------------------------------------------------------------------------------------------------------------------------

23. Write a query to display the employee id, employee name who have not issued with any item  in the year 2013. 
Hint: Exclude those employees who was never issued with any of the items in all the years. Display the records sorted in 
ascending order based on employee id.

A) SELECT DISTINCT e.employee_id,e.employee_name FROM 
   employee_master e JOIN employee_issue_details ei ON e.employee_id=ei.employee_id
    WHERE e.employee_id NOT IN (SELECT employee_id FROM employee_issue_details
    WHERE year(issue_date)='2013')
    ORDER BY employee_id;

-------------------------------------------------------------------------------------------------------------------------------

24. Write a query to display issue id, employee id, employee name, item id, item description and issue date.  
Display the data in descending order of date and then by issue id in ascending order.

A)  SELECT issue_id, eid.employee_id, employee_name, im.item_id, item_description,issue_date
    FROM employee_issue_details eid JOIN employee_master em ON eid.employee_id=em.employee_id
    JOIN item_master im ON eid.item_id=im.item_id
    ORDER BY issue_date DESC, issue_id;
    
----------------------------------------------------------------------------------------------------------------------------------

25. Write a query to display the employee id, employee name and total valuation for employee who has
issued maximum total valuation of the product. Give the alias name for total valuation as TOTAL_VALUATION.
[Hint: Suppose an employee E00019 issued item of price 5000, 10000, 12000 and E00020 issue item of price 2000, 7000, and 1000.
So the valuation of items taken by E00019 is 27000 and for E00020 it is 10000. So the employee id, employee name and total valuation 
of E00019 should display. ]

A) SELECT e.employee_id,em.employee_name,sum(i.item_valuation) TOTAL_VALUATION FROM
item_master i JOIN employee_issue_details e ON e.item_id=i.item_id
JOIN employee_master em ON em.employee_id=e.employee_id
GROUP BY e.employee_id HAVING sum(i.item_valuation)>=ALL(
SELECT sum(i.item_valuation) TOTAL_VALUATION FROM
item_master i JOIN employee_issue_details e ON e.item_id=i.item_id
JOIN employee_master em ON em.employee_id=e.employee_id
GROUP BY e.employee_id);

--------------------------------------------------------------------------------   ---------------------------------------------------------
















