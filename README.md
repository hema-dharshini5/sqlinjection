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
## Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img
![eth8 10](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/d0bd94c2-7608-4c5e-814e-0d3f11556864)
![eth 8 11](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/06a06b44-98d2-4977-906f-a4a533ab7bfd)
![eth 8 11](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/33334541-8789-40eb-a38d-22b3b11c43f6)
![eth8 13](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/ea79fdde-b333-4f21-8750-0b7e7bd20be2)
![eth 8 14](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/9370ac48-4c90-4849-af4b-f807d959a88c)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![eth 8 15](https://github.com/hema-dharshini5/sqlinjection/assets/147117728/d8b5f209-54a7-4e9c-a506-be4d04a092b9)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
