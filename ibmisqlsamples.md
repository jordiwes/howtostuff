# IBM i SQL Samples

## Select all spool files matching a specific spool file name - Basic
```
SELECT * FROM QSYS2.OUTPUT_QUEUE_ENTRIES_BASIC WHERE     
SPOOLED_FILE_NAME like 'LABINV'                          
```
## Select all spool files matching a specific spool file name - Extended
```
SELECT * FROM QSYS2.OUTPUT_QUEUE_ENTRIES WHERE     
SPOOLED_FILE_NAME like 'LABINV'                          
```

## Select object statistics for a library
```
SELECT * FROM TABLE                                   
(QSYS2.OBJECT_STATISTICS('QGPL','ALL')) AS A       
```
## Select object statistics for a library
```
SELECT * FROM TABLE                                   
(QSYS2.OBJECT_STATISTICS('QGPL','ALL')) AS A   
```
## Select object statistics for all libraries
```
SELECT * FROM TABLE (QSYS2.OBJECT_STATISTICS('*ALL','ALL')) AS A 
```
## Select TCP info for current connection. Good for getting local PC/Server client IP
```
SELECT * FROM QSYS2.TCPIP_INFO    
```
## Netstat Connection Info
```
SELECT * FROM QSYS2.NETSTAT_INFO 
```
## Netstat Connection Info. Check for Local Port 22 active on IPV4
```
SELECT * FROM QSYS2.NETSTAT_INFO WHERE 
CONNECTION_TYPE = 'IPV4' and local_port=22                                                        
```

## Select Active Jobs
https://www.rpgpgm.com/2015/11/getting-active-jobs-data-using-sql.html
https://www.rpgpgm.com/2019/07/extracting-jobs-name-from-job-name.html
https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzajq/rzajqudfactivejobinfo.htm
```
// Select all jobs
SELECT JOB_NAME,JOB_TYPE,JOB_STATUS,SUBSYSTEM,                   
           ELAPSED_CPU_PERCENTAGE AS PERCENT                     
FROM TABLE(QSYS2.ACTIVE_JOB_INFO(JOB_NAME_FILTER => '*ALL')) A   
ORDER BY ELAPSED_CPU_PERCENTAGE DESC

// Filtering by job status
SELECT JOB_NAME,JOB_TYPE,JOB_STATUS,SUBSYSTEM
    FROM TABLE(QSYS2.ACTIVE_JOB_INFO()) B
   WHERE JOB_STATUS = 'MSGW'
   ORDER BY JOB_NAME

// Filtering by job name
SELECT JOB_NAME,JOB_TYPE,JOB_STATUS,SUBSYSTEM,
         CPU_TIME
    FROM TABLE(QSYS2.ACTIVE_JOB_INFO()) C
   WHERE JOB_NAME LIKE '%SIMON%'
   ORDER BY CPU_TIME DESC

// Query and Parse Job Info and filter on 26 character JOB_NAME 
SELECT ORDINAL_POSITION AS ORD,                           
SUBSTR(JOB_NAME,                                          
LOCATE_IN_STRING(JOB_NAME,'/',-1)+1) as JOBNAME,          
       SUBSTR(JOB_NAME,                                   
LOCATE_IN_STRING(JOB_NAME,'/',1)+1,                       
(LOCATE_IN_STRING(JOB_NAME,'/',-1)-1)                     
- (LOCATE_IN_STRING(JOB_NAME,'/',1))) as JOBUSER,         
       SUBSTR(JOB_NAME,1,6) as JOBNUMBER,                 
JOB_TYPE as JOBTYPE,JOB_STATUS as JOBSTATUS,              
SUBSYSTEM                                                 
FROM                                                      
TABLE(QSYS2.ACTIVE_JOB_INFO(JOB_NAME_FILTER => '*ALL')) A 
where JOB_NAME LIKE '%%'                                        
```

## Select All Inquiry Messages from QSYSOPR Message Queue
Great way to monitor for selected messages and then respond
```
SELECT MESSAGE_QUEUE_LIBRARY, MESSAGE_QUEUE_NAME, MESSAGE_ID,       
MESSAGE_TYPE, MESSAGE_SUBTYPE,                                      
CAST(MESSAGE_TEXT AS VARCHAR(1024)) MESSAGE_TEXT, SEVERITY,          
MESSAGE_TIMESTAMP, MESSAGE_KEY, ASSOCIATED_MESSAGE_KEY, FROM_USER,  
FROM_JOB, FROM_PROGRAM, MESSAGE_FILE_LIBRARY, MESSAGE_FILE_NAME,    
MESSAGE_TOKENS,                                                     
CAST( MESSAGE_SECOND_LEVEL_TEXT as varchar(4096)) MESSAGE_SECOND_LEVEL_TEXT    
FROM QSYS2.MESSAGE_QUEUE_INFO WHERE MESSAGE_QUEUE_LIBRARY ='QSYS' and    
message_queue_name = 'QSYSOPR' and                                      
message_type = 'INQUIRY' 
```

## Set default shell to bash
Nowadays, the best way to do this is to using QSYS2.SET_PASE_SHELL_INFO() SQL procedure.

```
-- set current user's shell
CALL QSYS2.SET_PASE_SHELL_INFO('*CURRENT', '/QOpenSys/pkgs/bin/bash');

-- set a specific user's shell
-- (requires *SECADM special auth plus *USE and *OBJMGT to the user profile)
CALL QSYS2.SET_PASE_SHELL_INFO('THATUSER', '/QOpenSys/pkgs/bin/bash');

-- set the default shell which is returned for users that do not have
-- (requires *SECADM special auth plus *USE and *OBJMGT to QSYS)
CALL QSYS2.SET_PASE_SHELL_INFO('*DEFAULT', '/QOpenSys/pkgs/bin/bash');
```
https://stackoverflow.com/questions/23913957/set-default-pase-ibm-i-shell-for-individual-user
