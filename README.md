# bottleroad

### 개인적인 데이터를 정리하는 공간


# ORA-01455 ERROR 

## Symptoms

Occasionally, when making a GeoMedia Oracle connection to Oracle 12C database, the connection fails with following error message:

> ORA-01455 converting column overflows integer datatype

The error does not always occur and seems to be random.

## Diagnosis
GeoMedia obtains Oracle SESSIONID values for logging insert, update, and delete operations into GeoMedia modification log tables.
  

Oracle 12c introduced a new type of auditing called UNIFIED AUDITING which uses a different form of SESSIONID. Normally the SESSIONID comes from a sequence that recycles once SESSIONID 2,000,000,000 is reached. That is not the case if UNIFIED AUDITING is activated. In UNIFIED AUDITING, the SESSIONID's are randomly generated and can be much greater than the 2 billion limit on standard SESSIONID's. GeoMedia uses anINTEGER to store the retrieved SESSIONID and when that value exceeds the maxmimum value allowed for INTEGER ( 2,147,483,647) a connection error occurs:

> GMDatabase: PrepareStatement - pSQL: 'select userenv('SESSIONID') from dual'  
> Database Error Number: 1455  
> ORA-01455: converting column overflow integer  
> GOERROR - 8004076f  

Since the SESSIONID value is seemingly random, the connection errors only happen occasionally.

## Solution
To check to see if Unified auditing is turned on, run the following:

> SQL> select value from v$option where PARAMETER = 'Unified Auditing';
 

If FALSE is returned, then standard SESSIONID's are being used.   If the return is TRUE, then Unified Auditing is enabled and random connection errors are possible. By default in 12C, mixed mode auditing is enabled. For Unified Auditingto be active, a DBA would have had to deliberately enable it. There is no workaround to this problem other than to disable Unified Auditing in the database instance.


On most system, you can disable Unified Auditing by having the DBA disable the two default policies:
```
SQL> noaudit policy ORA_SECURECONFIG;
Noaudit succeeded.

SQL> noaudit policy ORA_LOGON_FAILURES;
Noaudit succeeded.
```
