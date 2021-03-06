# SQL
### Module 3


1./*Using a subquery, find the names of all the tracks for the album "Californication".*/


SELECT Name  
FROM Tracks  
WHERE AlbumId IN (SELECT AlbumId   
                  FROM Albums
               WHERE Title = "Californication")
               
 2./*Find the total number of invoices for each customer along with the customer's full name, city and email*/
 

SELECT SUM(i.InvoiceID) AS totalnumber, c.FirstName, c.LastName, c.Email  
From Invoices i INNER JOIN Customers c  
ON i.CustomerID =  c.CustomerID   
GROUP BY c.CustomerID 


3./*Retrieve the track name, album, artistID, and trackID for all the albums.*/


SELECT t.Name, t.TrackId, a.Title, a.ArtistId  
From Albums a LEFT JOIN Tracks t  
ON a.AlbumId =  t.AlbumId 


4. /*Retrieve a list with the managers last name, and the last name of the employees who report to him or her*/


SELECT M.LastName AS Manager,  
       E.LastName AS Employee  
       FROM Employees E, Employees M   
       WHERE E.ReportsTo = M.EmployeeID



5./*Find the name and ID of the artists who do not have albums.*/


SELECT Name,  
       a.ArtistId,  
       b.Title  
FROM Artists a  
LEFT JOIN Albums b  
ON a.ArtistId = b.ArtistId  
WHERE b.Title IS NULL


6. /*Use a UNION to create a list of all the employee's and customer's first names and last names ordered by the last name in descending order.*/


SELECT FirstName, LastName   
FROM Employees  
  UNION  
  SELECT FirstName, LastName   
  FROM Customers  
  ORDER BY LastName DESC

### Model 4

1. Pull a list of customer ids with the customer’s full name, and address, along with combining their city and country together.  
  
  SELECT CustomerId,  
         FirstName || " " || LastName AS FullName,  
         Address,  
         UPPER(City || " " || Country) AS CityCountry  
         FROM Customers  
           
2. Create a new employee user id by combining the first 4 letters of the employee’s first name with the first 2 letters of the employee’s last name. Make the new field lower case and pull each individual step to show your work.  
  
  SELECT LOWER(SUBSTR(FirstName, 1, 4)||SUBSTR(LastName, 1, 2)) AS EmployeeNewID,  
         LastName, FirstName  
         FROM Employees  
         
         
 3. Show a list of employees who have worked for the company for 15 or more years using the current date function. Sort by lastname ascending.  
 
SELECT LastName,FirstName,HireDate, date('now')-HireDate AS WorkY  
FROM Employees  
WHERE WorkY >= 15  
ORDER BY LastName ASC  

4. Profiling the Customers table, answer the following question.Are there any columns with null values? Indicate any below.   
  
SELECT *  
FROM Customers  
WHERE Phone IS NULL   
  
5.Find the cities with the most customers and rank in descending order.  
  
SELECT COUNT(CustomerID) AS Frequency,City  
FROM CUSTOMERS  
GROUP BY (City)  
ORDER BY Frequency DESC  
  
6.Create a new customer invoice id by combining a customer’s invoice id with their first and last name while ordering your query in the following order: firstname, lastname, and invoiceID.
  
 SELECT  c.FirstName, c.LastName,i.InvoiceId,  
         c.FirstName||c.LastName||i.InvoiceId AS NewID  
         FROM Customers c  
         INNER JOIN Invoices i  
         ON c.CustomerID = i.CustomerID  
         WHERE NewId like 'AstridGruber%'  
         ORDER BY c.FirstName,c.LastName, i.InvoiceId

 



