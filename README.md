# SQL-ORACLE-Example


### CREATE TABLE

#### Create table from copy another table

    CREATE TABLE TEMP_EMPLOYEE AS SELECT * FROM EMPLOYEE WHERE 1=2; 
    
#### Create table from copy another table and data

    CREATE TABLE TEMP_EMPLOYEE AS SELECT * FROM EMPLOYEE

#### Create table from copy another table with custom field

    CREATE TABLE TEMP_EMPLOYEE AS SELECT 
        emp_id           AS id,
        emp_code         AS code,
        emp_first_name   AS first_name,
        emp_last_name    AS last_name,
        manager_id      
    FROM EMPLOYEE WHERE 1=2; 
    /
    SELECT 
        emp_code,
        CASE 
            WHEN emp_first_name = 'Pratyaya' AND emp_last_name = 'Yeekhaday' THEN 'JAVA DEVELOPEE'
            WHEN emp_first_name = 'Smith'    AND emp_last_name = 'Ompang'    THEN 'JAVA DEVELOPEE'
            WHEN emp_first_name = 'Muhammad' AND emp_last_name = 'Lohmah'    THEN 'JAVA DEVELOPEE'
            ELSE 'PROGRAMMER'
        END AS POSITION
    FROM employee ORDER BY emp_code;
    
### CASE 

    SELECT 
        emp_code,
        emp_first_name,
        emp_last_name,
        CASE manager_id
            WHEN 1 THEN 'JAVA DEVELOPEE'
            WHEN 2 THEN 'PHP DEVELOPER'
            WHEN 3 THEN 'C# DEVELOPER'
            WHEN 4 THEN 'JS DEVELOPER'
            ELSE 'PROGRAMMER'
        END AS POSITION
    FROM employee ORDER BY emp_code;

### DECODE 

    SELECT 
        DECODE('Tirmizee','Tirmizee','Tirmizee','Sorry')
    FROM DUAL;

    SELECT 
        DECODE(
            EMP_CODE,
            'EM001','Tirmizee1',
            'EM002','Tirmizee2',
            'EM003','Tirmizee3',
            'EM004','Tirmizee4',
            'Sorry'
        )
    FROM employee  ORDER BY emp_code;

### DISTINCT

    SELECT DISTINCT * FROM employee;  -- No different SELECT * 
    SELECT DISTINCT emp_code FROM employee;
    SELECT DISTINCT emp_first_name, emp_last_name FROM employee;

### LPAD & RPAD 

### NVL 

### NVL2 

### COALESCE 

### SUBSTR 

### INTERSECT 

### MINUS

### UNION & UNION ALL

#### Using SUBSTR

    SELECT SUBSTR('Pratya Yeekhaday', 1, 1) FROM DUAL; --P
    SELECT SUBSTR('Pratya Yeekhaday', 1, 6) FROM DUAL; --Pratya
    SELECT SUBSTR('Pratya Yeekhaday', 3, 9) FROM DUAL; --atya Yeek

### CONCAT 

    CONCAT(string1,string2)
    
#### Using CONCAT

    SELECT CONCAT('Hello','World') FROM DUAL;                --HelloWorld
    SELECT CONCAT('Hello',CONCAT('World','2020')) FROM DUAL; --HelloWorld2020

    SELECT 'Hello' || 'World' FROM DUAL;                     --HelloWorld
    SELECT 'Hello' || 'World' || '2020' FROM DUAL;           --HelloWorld2020
