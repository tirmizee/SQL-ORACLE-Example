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

#### INSERT with VALUES

    INSERT INTO temp_employee(EMP_ID, EMP_CODE, EMP_FIRST_NAME, EMP_LAST_NAME) values(1,'EMP001','Pratya','Yeekhaday')

#### INSERT with SELECT

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

#### INSERT with Subqueries

    INSERT INTO employees2 (employee_id, employee_name, job, hiredate, salary)
    VALUES (8888, 'JONES','CLERK',to_date('17-12-1980','dd-mm-yyyy'),(SELECT MAX(salary)+1000 FROM employees));

### Operator

 - <b>=</b> : Equal.
 - <b><> or !=</b> : Not equal.
 - <b>></b> : Greater than.
 - <b><</b> : Less than.
 - <b>>=</b> : Great than or equal.
 - <b><=</b> : Less than or equal.

### DUAL

The DUAL table has one column named DUMMY whose data type is VARCHAR2() and contains one row with a value X.

#### DUAL with simple

    SELECT * FROM dual;

    SELECT 
        999,
        'Hello world'
    FROM DUAL;

### CASE 
    
    -- Switch
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
     -- If
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

    SELECT 
        UPPER('Pratya Yeekhaday'), -- PRATYA YEEKHADAY
        LOWER('Pratya Yeekhaday')  -- pratya yeekhaday
    FROM DUAL;

### SELECT

#### SELECT with simple

#### SELECT with CASE

    SELECT
        CASE value
            WHEN '1' THEN (SELECT COUNT(*) FROM employee)
            WHEN '2' THEN (SELECT COUNT(*) FROM users)
            WHEN '3' THEN (SELECT COUNT(*) FROM profile)
            ELSE (SELECT COUNT(*) FROM employee)
        END AS COUNT
    FROM app_setting;

#### SELECT with Column Alias

    SELECT 
        username AS usr,
        password AS psd
    FROM users;

    SELECT 
        username  usr,
        password  psd
    FROM users;

### GROUP BY

    SELECT
        column_list
    FROM
        T
    GROUP BY c1,c2,c3;

#### GROUP BY with simple 

    SELECT 
        COUNT(*) AS employee_count,
        AVG(e.salary) AS avg_salary,
        SUM(e.salary) AS sum_salary
    FROM employees e;

    SELECT 
        e.department_id,
        COUNT(*) AS employee_count,
        AVG(e.salary) AS avg_salary,
        SUM(e.salary) AS sum_salary
    FROM employees e
    GROUP BY e.department_id;

#### GROUP BY with multiple column

    SELECT 
        e.department_id,
        e.job,
        COUNT(*) AS employee_count,
        AVG(e.salary) AS avg_salary,
        SUM(e.salary) AS sum_salary
    FROM employees e
    GROUP BY 
        e.department_id,
        e.job;

#### GROUP BY with ORDER BY

    SELECT 
        e.department_id,
        COUNT(*) AS employee_count,
        AVG(e.salary) AS avg_salary,
        SUM(e.salary) AS sum_salary
    FROM employees e
    GROUP BY e.department_id
    ORDER BY e.department_id;

#### GROUP BY with JOIN

    -- INNER JOIN
    SELECT 
        d.department_name,
        COUNT(*) AS employee_count,
        AVG(e.salary) AS avg_salary,
        SUM(e.salary) AS sum_salary
    FROM departments d
    JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_name;
    -- LEFT JOIN
    SELECT 
        d.department_name,
        COUNT(e.employee_id)  AS employee_count,
        AVG(NVL(e.salary, 0)) AS avg_salary,
        SUM(NVL(e.salary, 0)) AS sum_salary
    FROM departments d
    LEFT OUTER JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_name;

#### GROUP BY with HAVING

    SELECT 
        d.department_name, 
        e.job,
        COUNT(e.employee_id) AS employee_count,
        AVG(NVL(e.salary, 0)) AS avg_salary,
        SUM(NVL(e.salary, 0)) AS sum_salary
    FROM departments d
    LEFT OUTER JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_name, e.job
    ORDER BY d.department_name, e.job;

    SELECT 
        d.department_name, 
        e.job,
        COUNT(e.employee_id) AS employee_count,
        AVG(NVL(e.salary, 0)) AS avg_salary,
        SUM(NVL(e.salary, 0)) AS sum_salary
    FROM departments d
    LEFT OUTER JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_name, e.job
    HAVING COUNT(e.employee_id) > 1
    ORDER BY d.department_name, e.job;

### ORDER BY

- <b>ASC</b> : Ascending 
- <b>DESC</b> : Descending 

#### ORDER BY with simple

    - Default order is ascending
    SELECT 
        * 
    FROM EMPLOYEES
    ORDER BY EMPLOYEE_NAME;

    SELECT 
        * 
    FROM EMPLOYEES
    ORDER BY EMPLOYEE_NAME ASC;

    SELECT 
        * 
    FROM EMPLOYEES
    ORDER BY EMPLOYEE_NAME DESC;

#### ORDER BY with multiple column

    select 
        * 
    from employees
    order by employee_name, jobb;

#### ORDER BY with different order

    SELECT 
        e.salary, 
        e.commission, 
        e.employee_name
    FROM employees e
    WHERE department_id = 30
    ORDER BY 
        e.salary ASC, 
        e.commission DESC;

#### ORDER BY with handling NULLs

    SELECT 
        e.commission, 
        e.employee_name
    FROM employees e
    WHERE department_id = 30
    ORDER BY e.commission ASC;
    /
    SELECT 
        e.commission, 
        e.employee_name
    FROM employees e
    WHERE department_id = 30
    ORDER BY e.commission ASC NULLS FIRST;


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

### CONNECT BY

### IN & NOT IN

    WHERE expression IN (Value 1, Value 2,…Value N)

    WHERE expression NOT IN (Value 1, Value 2,…Value N)

### EXISTS & NOT EXISTS

    WHERE EXISTS (sub-query)

    WHERE NOT EXISTS (sub-query)

### LIKE & NOT LIKE

### UNION & UNION ALL

- <b>UNION</b> : The UNION set operator returns all distinct rows selected by either query. That means any duplicate rows will be removed.
- <b>UNION ALL</b> : The UNION ALL set operator returns all rows selected by either query. That means any duplicates will remain in the final result set.

#### UNION with simple

    SELECT 
        department_id, 
        department_name
    FROM departments
    UNION
    SELECT 
        department_id, 
        department_name
    FROM departments

#### UNION ALL with simple

    SELECT 
        department_id, 
        department_name
    FROM departments
    UNION ALL
    SELECT 
        department_id, 
        department_name
    FROM departments

### INTERSECT 

The INTERSECT set operator returns all distinct rows selected by both queries. That means only those rows common to both queries will be present in the final result set.

#### INTERSECT with simple

    SELECT 
        department_id, 
        department_name
    FROM departments
    WHERE department_id <= 30
    INTERSECT
    SELECT 
        department_id, 
        department_name
    FROM departments
    WHERE department_id >= 20

### MINUS

The MINUS set operator returns all distinct rows selected by the first query but not the second. This is functionally equivalent to the ANSI set operator EXCEPT DISTINCT.

#### MINUS with simple

    SELECT 
        department_id, 
        department_name
    FROM departments
    WHERE department_id <= 30
    MINUS
    SELECT 
        department_id, 
        department_name
    FROM departments
    WHERE department_id >= 20;

### SEQUENCE 

### MIN & MAX

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

#### AVG with simple

    SELECT 
        AVG(sal) AS mean_sal
    FROM emp_salary;

#### AVG with GROUP BY

    SELECT 
        deptno,
        AVG(sal) AS mean_sal
    FROM emp_salary
    GROUP BY deptno
    ORDER BY deptno;

#### AVG with OVER PARTITION BY

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

    select 
        d.department_id,
        d.department_name,
        (select count(*) from employees e WHERE e.department_id = d.department_id) as count_employee
    from departments d;
    -- same as below
    SELECT
        d.department_id,
        d.department_name,
        count(e.employee_id) as count_employee
    from departments d
    LEFT join employees e on e.department_id = d.department_id
    GROUP BY 
        d.department_id,
        d.department_name
    ORDER BY d.department_id

### LISTAGG 

    LISTAGG (measure_column , ['delimiter']) WITHIN GROUP (order_by_clause) [OVER (query_partition_clause)]

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

    SELECT
        EXTRACT (YEAR FROM sysdate) YEAR,
        EXTRACT (MONTH FROM sysdate) MONTH,
        EXTRACT (DAY FROM sysdate) DAY,
        EXTRACT (YEAR FROM DATE '1999-12-31') DATE_FIX,
        EXTRACT (YEAR FROM CURRENT_TIMESTAMP) TIMESTAMP_YEAR,
        EXTRACT (MONTH FROM CURRENT_TIMESTAMP) TIMESTAMP_MONTH,
        EXTRACT (DAY FROM CURRENT_TIMESTAMP) TIMESTAMP_DAY,
        EXTRACT (HOUR FROM CURRENT_TIMESTAMP) TIMESTAMP_HOUR,
        EXTRACT (MINUTE FROM CURRENT_TIMESTAMP) TIMESTAMP_MINUTE,
        EXTRACT (SECOND FROM CURRENT_TIMESTAMP) TIMESTAMP_SECOND,
        EXTRACT( HOUR FROM TIMESTAMP '1999-12-31 23:59:59.10' ) TIMESTAMP_MONTH_FIX,
        EXTRACT (YEAR FROM TO_DATE( '31-Dec-1999 15:30:20 ',  'DD-Mon-YYYY HH24:MI:SS' )) TO_DATE_YEAR
    FROM DUAL;

### WITH 

An alternative to an inline view is to move the subquery out to the WITH clause. We can then reference this named query in the FROM clause of the main SELECT statement. This can be used to make a very complicated FROM clause look much simpler.

#### WITH with simple

    SELECT 
        e.employee_name, 
        d.department_name
    FROM employees e
    JOIN departments d ON d.department_id = e.department_id
    ORDER BY e.employee_name;

    SELECT 
        e.employee_name, 
        d.department_name
    FROM employees e, departments d
    WHERE d.department_id = e.department_id
    ORDER BY e.employee_name;

    SELECT 
        ed.employee_name, 
        ed.department_name
    FROM (
        SELECT 
            e.employee_name, 
            d.department_name
        FROM employees e, departments d
        WHERE d.department_id = e.department_id
    ) ed
    ORDER BY ed.employee_name;

    WITH emp_dept_join AS (
        SELECT 
            e.employee_name, 
            d.department_name
        FROM employees e, departments d
        WHERE d.department_id = e.department_id
    )
    SELECT 
        ed.employee_name, 
        ed.department_name
    FROM emp_dept_join ed
    ORDER BY ed.employee_name;

#### WITH with multiple

### TRUNC

The TRUNC (date) function is used to get the date with the time portion of the day truncated to a specific unit of measure. 

    TRUNC(date , [fmt])

#### TRUNC with simple

    SELECT 
        TRUNC(TO_DATE('02-MAR-15 15:35:32', 'DD-MON-YY HH24:MI:SS')),
        TRUNC(TO_DATE('02-MAR-15 15:35:32', 'DD-MON-YY HH24:MI:SS'), 'DD') ,
        TRUNC(TO_DATE('02-MAR-15 15:35:32', 'DD-MON-YY HH24:MI:SS'), 'MM') ,
        TRUNC(TO_DATE('02-MAR-15 15:35:32', 'DD-MON-YY HH24:MI:SS'), 'YEAR') 
    FROM DUAL;

### TRUNCATE 

    TRUNCATE TABLE schema_name.table_name
    [CASCADE]
    [[ PRESERVE | PURGE] MATERIALIZED VIEW LOG ]]
    [[ DROP | REUSE]] STORAGE ]

#### TRUNCATE with simple 

    TRUNCATE TABLE temp_employee;

### Top-N Queries

    CREATE TABLE rownum_order_test (
      val  NUMBER
    );

    INSERT ALL
      INTO rownum_order_test
      INTO rownum_order_test
    SELECT level
    FROM   dual
    CONNECT BY level <= 10;

#### Rownum with simple

    SELECT 
        val
    FROM rownum_order_test
    WHERE rownum <= 5

#### Rownum with ORDER BY

    SELECT
        val
    FROM (
        SELECT 
            val
        FROM rownum_order_test
        ORDER BY val
    ) WHERE rownum <= 5

#### Rownum with paging

    SELECT  username FROM (
        SELECT username, rownum AS rnum FROM (
            SELECT username
            FROM users
            ORDER BY username
        ) WHERE rownum < :v_start + :v_limit)
    WHERE rnum >= :v_start;

### CONCAT 

    CONCAT(string1,string2)
    
#### CONCAT with simple

    SELECT CONCAT('Hello','World') FROM DUAL;                --HelloWorld
    SELECT CONCAT('Hello',CONCAT('World','2020')) FROM DUAL; --HelloWorld2020

    SELECT 'Hello' || 'World' FROM DUAL;                     --HelloWorld
    SELECT 'Hello' || 'World' || '2020' FROM DUAL;           --HelloWorld2020
    
### Reference

- https://oracle-base.com/articles/sql/articles-sql#getting-started
