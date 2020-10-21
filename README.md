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

### DUAL

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

### UPPER & LOWER

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

#### TO_NUMBER with simple

    SELECT 
        TO_NUMBER('1210.73', '9999.99'),
        TO_NUMBER('546', '9999.99')
    FROM DUAL;

### CAST 

### UNION & UNION ALL

### SEQUENCE 

### MIN & MAX

    CREATE TABLE emp (
      empno    NUMBER(4) CONSTRAINT pk_emp PRIMARY KEY,
      ename    VARCHAR2(10),
      job      VARCHAR2(9),
      mgr      NUMBER(4),
      hiredate DATE,
      sal      NUMBER(7,2),
      comm     NUMBER(7,2),
      deptno   NUMBER(2)
    );

    INSERT INTO emp_salary VALUES (7369,'SMITH','CLERK',7902,to_date('17-12-1980','dd-mm-yyyy'),800,NULL,20);
    INSERT INTO emp_salary VALUES (7499,'ALLEN','SALESMAN',7698,to_date('20-2-1981','dd-mm-yyyy'),1600,300,30);
    INSERT INTO emp_salary VALUES (7521,'WARD','SALESMAN',7698,to_date('22-2-1981','dd-mm-yyyy'),1250,500,30);
    INSERT INTO emp_salary VALUES (7566,'JONES','MANAGER',7839,to_date('2-4-1981','dd-mm-yyyy'),2975,NULL,20);
    INSERT INTO emp_salary VALUES (7654,'MARTIN','SALESMAN',7698,to_date('28-9-1981','dd-mm-yyyy'),1250,1400,30);
    INSERT INTO emp_salary VALUES (7698,'BLAKE','MANAGER',7839,to_date('1-5-1981','dd-mm-yyyy'),2850,NULL,30);
    INSERT INTO emp_salary VALUES (7782,'CLARK','MANAGER',7839,to_date('9-6-1981','dd-mm-yyyy'),2450,NULL,10);
    INSERT INTO emp_salary VALUES (7788,'SCOTT','ANALYST',7566,to_date('13-JUL-87','dd-mm-rr')-85,3000,NULL,20);
    INSERT INTO emp_salary VALUES (7839,'KING','PRESIDENT',NULL,to_date('17-11-1981','dd-mm-yyyy'),5000,NULL,10);
    INSERT INTO emp_salary VALUES (7844,'TURNER','SALESMAN',7698,to_date('8-9-1981','dd-mm-yyyy'),1500,0,30);
    INSERT INTO emp_salary VALUES (7876,'ADAMS','CLERK',7788,to_date('13-JUL-87', 'dd-mm-rr')-51,1100,NULL,20);
    INSERT INTO emp_salary VALUES (7900,'JAMES','CLERK',7698,to_date('3-12-1981','dd-mm-yyyy'),950,NULL,30);
    INSERT INTO emp_salary VALUES (7902,'FORD','ANALYST',7566,to_date('3-12-1981','dd-mm-yyyy'),3000,NULL,20);
    INSERT INTO emp_salary VALUES (7934,'MILLER','CLERK',7782,to_date('23-1-1982','dd-mm-yyyy'),1300,NULL,10);
    COMMIT;

#### MIN & MAX syntax

    MIN([ DISTINCT | ALL ] expr) [ OVER (analytic_clause) ]
    MAX([ DISTINCT | ALL ] expr) [ OVER (analytic_clause) ]

#### MIN & MAX with simple

    SELECT  MIN(sal) FROM emp_salary;
    SELECT  MIN(NVL(sal,0)) FROM emp_salary;
    SELECT  MIN(DISTINCT NVL(sal,0)) FROM emp_salary;
    
    SELECT  MAX(sal) FROM emp_salary;
    SELECT  MAX(NVL(sal,0)) FROM emp_salary;
    SELECT  MAX(DISTINCT NVL(sal,0)) FROM emp_salary;

#### MIN & MAX with GROUP BY

    SELECT 
        deptno,
        MIN(sal) AS min_sal
    FROM  emp_salary
    GROUP BY deptno
    ORDER BY deptno;
    
    SELECT 
        deptno,
        MAX(sal) AS min_sal
    FROM  emp_salary
    GROUP BY deptno
    ORDER BY deptno;

#### MIN & MAX with OVER PARTITION BY

    SELECT 
        empno,     
        ename,
        deptno,
        sal,
        MIN(sal) OVER (PARTITION BY deptno) AS min_sal
    FROM emp_salary
    ORDER BY deptno;
    
    SELECT 
        empno,     
        ename,
        deptno,
        sal,
        MAX(sal) OVER (PARTITION BY deptno) AS min_sal
    FROM emp_salary
    ORDER BY deptno;

### SUM

#### SUM with simple

    SELECT 
        SUM(sal)
    FROM emp_salary;

#### SUM with GROUP BY

    SELECT 
        deptno,
        SUM(sal)
    FROM emp_salary
    GROUP BY deptno
    ORDER BY deptno;

#### SUM with OVER PARTITION BY

    SELECT 
        empno,
        ename,
        deptno,
        sal,
        SUM(sal) OVER (PARTITION BY deptno) AS total_sal_by_dept
    FROM emp_salary;
    
    SELECT 
        empno,
        ename,
        deptno,
        sal,
        SUM(sal) OVER (PARTITION BY deptno ORDER BY sal) AS total_sal_by_dept
    FROM emp_salary;

### AVG

### AVG with simple

    SELECT 
        AVG(sal) AS mean_sal
    FROM emp_salary;

### AVG with GROUP BY

    SELECT 
        deptno,
        AVG(sal) AS mean_sal
    FROM emp_salary
    GROUP BY deptno
    ORDER BY deptno;

### AVG with OVER PARTITION BY

    SELECT
        empno,
        ename,
        deptno,
        sal,
        AVG(sal) OVER (PARTITION BY deptno) AS mean_sal_by_dept
    FROM emp_salary;

### COUNT

#### COUNT with simple

    SELECT COUNT(*) FROM employee;

    SELECT
        (SELECT COUNT(*) FROM employee) AS count_of_employee,
        (SELECT COUNT(*) FROM users)    AS count_of_users,
        (SELECT COUNT(*) FROM profile)  AS count_of_profile
    FROM DUAL;
    
#### COUNT field 

    SELECT 
        COUNT(*) AS count_total,
        COUNT(sal) AS count_sal,
        COUNT(comm) AS count_comm
    FROM emp_salary;

#### COUNT field with GROUP BY

    SELECT
        deptno,
        COUNT(*) AS count_total,
        COUNT(sal) AS count_sal,
        COUNT(comm) AS count_comm
    FROM emp_salary
    GROUP BY deptno
    ORDER BY deptno;

#### COUNT with OVER PARTITION BY

    SELECT
        empno,
        ename,
        deptno,
        sal,
        COUNT(*) OVER (PARTITION BY deptno) AS amount_by_dept
    FROM emp_salary;

#### COUNT with Subquery

### LISTAGG 

#### LISTAGG with simple

    SELECT 
        LISTAGG(ename, ',') WITHIN GROUP (ORDER BY ename) AS employees
    FROM emp_salary where deptno = 20

    SELECT 
        deptno, 
        LISTAGG(ename, ',') WITHIN GROUP (ORDER BY ename) AS employees
    FROM emp_salary
    GROUP BY deptno
    ORDER BY deptno;

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
    
### Reference

- https://oracle-base.com/articles/12c/row-limiting-clause-for-top-n-queries-12cr1
- https://oracle-base.com/articles/misc/sql-for-beginners-the-select-list
