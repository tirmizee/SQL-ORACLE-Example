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

COALESCE function aims to return a non-NULL value. You must specify at least two expressions.

#### COALESCE syntax

    COALESCE ( expr1, expr2, [expr…])

#### COALESCE with simple

    SELECT
        COALESCE(emp_code, name ) AS COALESCE
    FROM salary;
    -- is equivalent to
    SELECT
        CASE WHEN emp_code IS NOT NULL THEN emp_code ELSE name END
    FROM salary;

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

### TO_CHAR

- <b>NLS_CALENDAR</b> indicates the calendar system used for the language
- <b>NLS_DATE_LANGUAGE</b> specifies the language for days, months

#### TO_CHAR syntax

    TO_CHAR( input_value, [format_mask], [nls_parameter] )

#### TO_CHAR with simple

    SELECT 
        TO_CHAR(sysdate, 'yyyy'),
        TO_CHAR(sysdate, 'mm/yyyy'),
        TO_CHAR(sysdate, 'dd/mm/yyyy'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH12'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH24'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH:MI'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH:MI:SS'),
        TO_CHAR(sysdate, 'dd/mm/yyyy HH:MI:SS', 'NLS_CALENDAR=''THAI BUDDHA'''),
        TO_CHAR(sysdate, 'Day Month yyyy HH:MI:SS', 'NLS_CALENDAR=''THAI BUDDHA'' NLS_DATE_LANGUAGE=THAI')
    FROM DUAL;

    SELECT 
        TO_CHAR(SYSDATE, 'Month'),
        TO_CHAR(SYSDATE, 'MONTH'),
        TO_CHAR(SYSDATE, 'Year'),
        TO_CHAR(SYSDATE, 'YEAR'),
        TO_CHAR(SYSDATE, 'Day'),
        TO_CHAR(SYSDATE, 'DAY'),
        TO_CHAR(SYSDATE, 'WW')
    FROM DUAL;

    SELECT 
        TO_CHAR(12345, '00000000'),
        TO_CHAR(12345.67, '99999.9')
    FROM DUAL;

### TO_DATE

#### TO_DATE syntax

    TO_DATE( string1 , [format_mask] , [nls_language] )

#### TO_DATE with simple

    SELECT 
        TO_DATE('20020315', 'yyyymmdd'),
        TO_DATE('2003/07/09', 'yyyy/mm/dd'),
        TO_DATE('2012-06-05', 'YYYY-MM-DD'),
        TO_DATE('2015/05/15 8:30:25', 'YYYY/MM/DD HH:MI:SS'),
        TO_DATE('21-10-2563', 'dd-mm-yyyy','NLS_CALENDAR=''THAI BUDDHA'''),
        TO_DATE('21-10-2563', 'dd-mm-yyyy','NLS_DATE_LANGUAGE = THAI')
    FROM DUAL;

### TO_NUMBER 

#### TO_NUMBER syntax

    TO_NUMBER(string1, [format_mask], [nls_language])

### CAST 

### UNION & UNION ALL

### SEQUENCE 

### COUNT

#### COUNT with simple

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

#### CONCAT syntax

    CONCAT(string1,string2)
    
#### CONCAT with simple

    SELECT CONCAT('Hello','World') FROM DUAL;                --HelloWorld
    SELECT CONCAT('Hello',CONCAT('World','2020')) FROM DUAL; --HelloWorld2020

    SELECT 'Hello' || 'World' FROM DUAL;                     --HelloWorld
    SELECT 'Hello' || 'World' || '2020' FROM DUAL;           --HelloWorld2020
