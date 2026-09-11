CREATE TABLE EMPLOYEE (
    EMP_ID NUMBER PRIMARY KEY,
    EMP_NAME VARCHAR2(50),
    SALARY NUMBER
);
INSERT INTO EMPLOYEE VALUES (1, 'Rahul', 30000);
INSERT INTO EMPLOYEE VALUES (2, 'Priya', 40000);
INSERT INTO EMPLOYEE VALUES (3, 'Aman', 25000);
INSERT INTO EMPLOYEE VALUES (4, 'Neha', 0);
INSERT INTO EMPLOYEE VALUES (5, 'Riya', 50000);

COMMIT;
SELECT * FROM EMPLOYEE;
SET SERVEROUTPUT ON;

DECLARE

    -- Declare explicit cursor
    CURSOR emp_cursor IS
        SELECT EMP_ID, SALARY
        FROM EMPLOYEE;

    -- Variables to store fetched values
    V_EMP_ID EMPLOYEE.EMP_ID%TYPE;
    V_SALARY EMPLOYEE.SALARY%TYPE;

    -- User-defined exception
    SALARY_ZERO EXCEPTION;

BEGIN

    -- Open the cursor
    OPEN emp_cursor;

    -- Fetch first record
    FETCH emp_cursor INTO V_EMP_ID, V_SALARY;

    -- Continue while records are available
    WHILE emp_cursor%FOUND
    LOOP

        -- Check if salary is zero
        IF V_SALARY = 0 THEN
            RAISE SALARY_ZERO;
        END IF;

        -- Increase salary by 10%
        UPDATE EMPLOYEE
        SET SALARY = SALARY * 1.10
        WHERE EMP_ID = V_EMP_ID;

        -- Fetch next record
        FETCH emp_cursor INTO V_EMP_ID, V_SALARY;

    END LOOP;

    -- Close the cursor
    CLOSE emp_cursor;

EXCEPTION

    -- Handle zero salary
    WHEN SALARY_ZERO THEN
        DBMS_OUTPUT.PUT_LINE(
            'Salary is zero. Increment not possible.'
        );

END;
/