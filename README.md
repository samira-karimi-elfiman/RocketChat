# RocketChat

Application: RocketChat 3.0.1 (web)
Weakness:	Insecure Direct Object Reference (IDOR)
Reported Date: Apr 7, 2020
Disclosed Date:	June 14, 2020

# What was the Problem?
I find user reset password hash info and other security info on "/api/v1/users.info" with low level user 

# Impact
account takeover

# How do I fix it?:
rocketchat has a fix for this: https://github.com/RocketChat/Rocket.Chat/pull/17238

update your application

# Exploit:
note1: I login on rocketchat with ldap account (my role : user)

note2: in request "https://target/api/v1/users.info?username=[x]" you should change username to userId

1- please login with user ldap account (role user)

2- send a request to https://target/api/v1/users.list and copy _id value

3- send a request to https://target/api/v1/users.info?userId=[userId] and copy email value (in response you can see important security information )

4- logout and click "forget your password" link on https://target/home and send an email to above email address that you copied

5- login with Your account and send a request to https://target/api/v1/users.list and search the same email in response and copy _id value

6- send a request to https://target/api/v1/users.info?userId=[userId] and copy reset hash value

7- logout your account and send a request to https://target/reset-password/[reset_hash]

8- set new password

9- login and enjoy
