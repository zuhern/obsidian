---
Created: Invalid date
Updated: Invalid date
---
[http://www.cyberciti.biz/faq/how-do-i-start-oracle-service-in-unix/](http://www.cyberciti.biz/faq/how-do-i-start-oracle-service-in-unix/)

**How To Startup Oracle Database on a Unix/Linux**

Use the su - username command to login as oracle user. Open the Terminal or login using ssh and type the following command to login`**$ su - oracle**`

### Start Oracle server in UNIX/Linux

Now, use the lsnrctl command to start service (usually located at /home/oracle/oracle/product/10.2.0/db_1/bin directory):`**$ lsnrctl start**`  
Next start database:  
`$ dbstart`  
If above is not working try to login as sysdba:  
`$ sqlplus '/ as sysdba'`  
At   
SQL> type startup command:

```Plain
startup
```

## **Stop Oracle service in UNIX/Linux**

To stop Oracle service type following two commands:`$ lsnrctl stop $ dbshut`  
If above failed login as sysdba user:  
`$ sqlplus '/ as sysdba'`  
At   
SQL> type shutdown command:

```Plain
shutdown
```