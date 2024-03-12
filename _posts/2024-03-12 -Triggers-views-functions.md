#### Introduction
Why are Triggers,views and functions  important particularly to database administrators whose work is to maintain databases and ensure that information is kept under wraps?

Also why are they important to data analysts particularly when we are investigating data using database languages such as SQL,Postgresql.

So you are probably wondering ?


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/blu7ul1wiam4021sc0gq.png)

I will show you Let's us start with the definition of each term

## <u>View</u> 
- A view is a virtual table that you can create by using a saved query.Views are handy for example when you don't want the database containing your dataset you uploaded to be tampered with or any adjustment to be made without prior permission.

- I normally think of views like this🤔.Whenever you are repeating the same operation over and over especially if it is the same row and columns you are querying this is what you use.

- Instead of going over and over and over writing the same code 🔄
- We use views ⬇️

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/upupo8xdxe6kxn4tp3ui.png)


Therefore we can summarise the importance of views through these points:
- Simplicity to avoid complexity
- Provide security
- Avoid duplication 

The syntax of view is as follows:

```
create or replace view view_name as
select column1,column_2
from your_dataset_in_your_table

```
For example:
- Lets say we want to change the information of a particular sales department in our 'sales dataset containing the following columns:

          - ✔️ Sales_name
          - ✔️ Sales_id
          - ✔️ Sales_company


- We want to change only the sales_id of a particular company and not interfere with the other rows in the dataset we use can do this ⬇️ 

```
create or replace view sales_view_name_you_want
select sales_name,
sales_company
from sales_dataset
where sales_id =1
with local check option

```
_with local check option_ restricts any update done on the view that does not follow the parameters of the view i.e it can't update the view with sales_id = 2.
- This is is the form of data security that is essential in keeping track of the database and also ensure that changes are monitored.
- Okay now that we have learned this let's see what we can do in terms of ⏭️ CRUD operations ➡️ Create,Read,Update or delete.

### <u>UPDATE</u>

```
## We can decide to update the particular view 👐
update sales_view_name_you_want
set company_name = 'Bobbyaxelrod99'
where sales_id = 1

```
### <u>INSERT</u>

```
Insert into sales_view_name_you_want (sales_name,sales_company,sales_id)
values ('jordan','Apple',1)

insert into sales_view_name_you_want(sales_name,sales_company,sales_id)
values ('John',''Amazon',2)

```
- The first query in the insert operation above ⬆️ runs while the second query doesn't why?
- Remember our _with local check option_ that we had inserted before in the first code.This restricts our changes to only sales_id = 1
- The same logic applies to other CRUD operations that we might want to introduce.
- All in all views buffers up 💪🏼 security in our dataset while aslo helping us to control what takes place in our dataset.

⏭️ Lets move to functions.

## <u>Functions</u>
 - Functions are used in Postgresql just the way we use them in 
  other programming languages.They are used as shortcuts when 
  conducting operations in programming.

Examples of functions in Postgresql include: 

- sum() 

- lower() 

- upper() 

We have to first understand the syntax of a function in Postgresql. 

```
create or replace function 
function_name( column_name1 numeric,column_name2 numeric,
              places_of_decimals integer default 1)
returns numeric as
' select ( column_name1 - column_name2)::,places_of_decimals);'
language sql
immutable
returns null or null input
```
The function above can be explained as follows :
- _function_name_- this is the name of the function which contains 
  a list of arguments.Each argument in the parenthensis has a data 
  type.
- _default 1_ - indicates that we want only one value to be 
  displayed.
- _returns numeric_ - returns the function as numeric
- _language sql_ - it pecifies that it is written in sql
- _immutable_ - it indicates that the function won't be making any 
  changes to the database.

### <u>So how do we know it works?</u>🤔
- We can check the function if it works by simply :

```
select function_name(argument1,argument2)

```

After Views and functions we can now move on to ⏭️ triggers.

## **<u>Triggers</u>**

What are triggers?
- Triggers in a database are used to execute a function when a 
 specified event occurs like a CRUD operation such as 
 insert,delete,update.
- We can set a trigger right before,after,instead of an event 
 occuring.It is used as a shortcut particularly when we have a 
 large query that executes a given operation one by one.
- The power of triggers is that it helps us to execute a given instruction all at once. 

The **first step** in creating triggers is to first create a function 

```
create or replace function _trigger_name_()
returns trigger as
$$
begin
➡️ (your statement depending on the CRUD operation you are performing)

Return NEW;
END;
$$ LANGUAGE plpgsql
```
The **second step** you create a trigger also depending on your CRUD operation

```
create trigger _trigger_you_want_
after (CRUD Operation you want to perform)
ON _interested_row_you_want_to_be_manipulated_
for each row
execute procedure _trigger_name_ ()
```
* Keep in mind that we can use the following after,before or even instead depending on your perfernce and also your situation

### **<u>Conclusion</u>**
- All in all views,functions and also triggers are important tools to use when you are scrutinizing data the mastery of each tool takes time to learn.

- It is mainly used by database administrators but as a data analyst I find it useful in making my life a little bit easier.  




  
  




