# nifi-quickstart-ddl-backup
Apache NiFi to backup Snowflake DDL for a database

![image](https://github.com/user-attachments/assets/3b54e6f7-c7bb-40e1-b275-76e3a481cba8)





#### Flow

1. ExecuteSQLRecord      SELECT GET_DDL('DATABASE',  'DEMO') as FIELDS;

![image](https://github.com/user-attachments/assets/2bce93b4-ae84-425e-8f80-9b5f72270c2d)


2. SplitRecord           JSON Reader, JSON Writer, 1 row

![image](https://github.com/user-attachments/assets/2d94cede-281f-4535-ba73-25de97da57b8)

   
3. EvaluateJsonPath      flowfile-attribute, json, ignore, sql = $.FIELDS

![image](https://github.com/user-attachments/assets/6f771fa8-6561-4785-9b56-b886c0ef9ae7)


4. ReplaceText           Regex Replace, (?s:^.*$), ${sql}, Entire Text, All

![image](https://github.com/user-attachments/assets/fb98562f-8432-4489-ad56-54ac26754476)


5. ChunkText             Recursive Delimiters, 4000, true, ;

![image](https://github.com/user-attachments/assets/bce73c18-eca8-42f1-b1f4-50327735ab5a)


6. <Options>             ExecuteSQLStatement, PutSlack, PutS3, PutFile, ...


![image](https://github.com/user-attachments/assets/3f40ba3c-bb4a-4d91-b966-0d92a6fb18e5)



![image](https://github.com/user-attachments/assets/53bbe797-971f-44b6-a1e6-d64bb31a00ae)

