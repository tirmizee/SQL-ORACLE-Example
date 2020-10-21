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

### INSERT

#### Using INSERT with VALUES

    INSERT INTO temp_employee(EMP_ID, EMP_CODE, EMP_FIRST_NAME, EMP_LAST_NAME) values(1,'EMP001','Pratya','Yeekhaday')

#### Using INSERT with SELECT

    INSERT INTO temp_employee  SELECT * FROM employee; 

    INSERT INTO temp_employee(
        emp_id,
        emp_code,
        emp_first_name,
        emp_last_name
    )  SELECT 
        ROWNUM,
        u.username,
        p.first_name,
        p.last_name
    FROM users u
    INNER JOIN profile p ON u.profile_id = p.profile_id; 

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

#### LPAD & RPAD syntax

    LPAD( string1, padded_length , [pad_string] )
    RPAD( string1, padded_length , [pad_string] )

#### LPAD with simple

    SELECT
        LPAD('999',3),     -- 999
        LPAD('999',7),     --     999
        LPAD('999',7,'0')  -- 0000999
    FROM dual;

#### RPAD with simple

    SELECT
        RPAD('999',3),     -- 999
        RPAD('999',7),     -- 999
        RPAD('999',7,'0')  -- 9990000
    FROM dual;

### NVL 

#### NVL syntax

    NVL (exp, replacement-exp)

#### NVL with simple

    CREATE TABLE salary (
        id NUMBER(19,0),
        emp_code NVARCHAR2(50),
        salary NUMBER(10,2) NOT NULL
    );

    insert into salary SELECT
        ROWNUM,
        employee.emp_code,
        dbms_random.value(1,50000)
    from employee where ROWNUM <= 100;

    SELECT
        NVL(salary,0) + 100 AS total
    FROM salary;

    SELECT
        NVL(emp_code,'XXX') AS CODE
    FROM salary


### NVL2 

#### NVL2 syntax

    NVL2( string1, value_if_not_null, value_if_null )

#### NVL2 with simple

    SELECT
        NVL2(salary,1000,0) AS total
    FROM salary;

    SELECT
        NVL2(emp_code,'NOT NULL','IS NULL') AS CODE
    FROM salary

### COALESCE 

COALESCE function aims to return a non-NULL value

#### COALESCE syntax

    COALESCE ( expr1, expr2, [expr…])

### SUBSTR 

    SELECT SUBSTR('Pratya Yeekhaday', 1, 1) FROM DUAL; --P
    SELECT SUBSTR('Pratya Yeekhaday', 1, 6) FROM DUAL; --Pratya
    SELECT SUBSTR('Pratya Yeekhaday', 3, 9) FROM DUAL; --atya Yeek

### SELECT

    SELECT
        CASE value
            WHEN '1' THEN (SELECT COUNT(*) FROM employee)
            WHEN '2' THEN (SELECT COUNT(*) FROM users)
            WHEN '3' THEN (SELECT COUNT(*) FROM profile)
            ELSE (SELECT COUNT(*) FROM employee)
        END AS COUNT
    FROM app_setting;

### INTERSECT 

### MINUS

### UNION & UNION ALL

### SEQUENCE 

### COUNT

#### Using COUNT

    SELECT COUNT(*) FROM employee;

    SELECT
        (SELECT COUNT(*) FROM employee) AS count_of_employee,
        (SELECT COUNT(*) FROM users)    AS count_of_users,
        (SELECT COUNT(*) FROM profile)  AS count_of_profile
    FROM DUAL;

### MAX & MIN

### SUM

### EXTRACT

### TRUNCATE 

    TRUNCATE TABLE schema_name.table_name
    [CASCADE]
    [[ PRESERVE | PURGE] MATERIALIZED VIEW LOG ]]
    [[ DROP | REUSE]] STORAGE ]

#### Using TRUNCATE

    TRUNCATE TABLE temp_employee;


### CONCAT 

    CONCAT(string1,string2)
    
#### Using CONCAT

    SELECT CONCAT('Hello','World') FROM DUAL;                --HelloWorld
    SELECT CONCAT('Hello',CONCAT('World','2020')) FROM DUAL; --HelloWorld2020

    SELECT 'Hello' || 'World' FROM DUAL;                     --HelloWorld
    SELECT 'Hello' || 'World' || '2020' FROM DUAL;           --HelloWorld2020
