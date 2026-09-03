CREATE DATABASE customer_db;
USE customer_db;

CREATE TABLE customers (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    address VARCHAR(200),
    salary DECIMAL(10,2)
);

INSERT INTO customers (id, name, age, address, salary)
VALUES
(1, 'Arun', 25, 'Chennai', 25000),
(2, 'Rahul', 30, 'Bangalore', 30000),
(3, 'Priya', 28, 'Coimbatore', 28000),
(4, 'Anjali', 35, 'Madurai', 35000),
(5, 'Vijay', 27, 'Trichy', 27000);

DELIMITER //

CREATE PROCEDURE implicit_cursor()
BEGIN
    DECLARE total_rows INT;

    UPDATE customers
    SET salary = salary + 500;

    SET total_rows = ROW_COUNT();

    IF total_rows = 0 THEN
        SELECT 'No customers selected' AS Message;
    ELSE
        SELECT CONCAT(total_rows, ' customers selected') AS Message;
    END IF;
END //

DELIMITER ;

CALL implicit_cursor();
SELECT * FROM customers;



DELIMITER //

CREATE PROCEDURE explicit_cursor()
BEGIN
    DECLARE c_id INT;
    DECLARE c_name VARCHAR(100);
    DECLARE c_addr VARCHAR(200);
    DECLARE done INT DEFAULT 0;

    DECLARE c_customers CURSOR FOR
        SELECT id, name, address
        FROM customers;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET done = 1;

    OPEN c_customers;

    read_loop: LOOP

        FETCH c_customers
        INTO c_id, c_name, c_addr;

        IF done = 1 THEN
            LEAVE read_loop;
        END IF;

        SELECT CONCAT(c_id, ' ', c_name, ' ', c_addr) AS Customer_Details;

    END LOOP;

    CLOSE c_customers;
END //

DELIMITER ;

CALL explicit_cursor();
