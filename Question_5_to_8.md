1️⃣ IF-ELSE Control Structure
Procedure: Check Student Rank Category

DELIMITER //

CREATE PROCEDURE Check_Rank_Category(
    IN p_form_no CHAR(6),
    OUT rank_category VARCHAR(20)
)
BEGIN
    DECLARE r INT;

    SELECT ccat_rank INTO r
    FROM CCAT_Result
    WHERE form_no = p_form_no;

    IF r <= 100 THEN
        SET rank_category = 'Top Rank';
    ELSEIF r <= 500 THEN
        SET rank_category = 'Medium Rank';
    ELSE
        SET rank_category = 'Low Rank';
    END IF;

END //

DELIMITER ;

Result :
<img width="732" height="335" alt="image" src="https://github.com/user-attachments/assets/e4c79f2f-b65b-4a4b-8f20-d70f0604ece9" />

2️⃣ CASE Control Structure
Procedure: Freeze Status Display
DELIMITER //

CREATE PROCEDURE Check_Freeze_Status(
    IN p_pref_id INT
)
BEGIN
    DECLARE status BOOLEAN;

    SELECT freeze INTO status
    FROM Preferences
    WHERE preference_id = p_pref_id;

    SELECT 
    CASE
        WHEN status = TRUE THEN 'Seat Frozen'
        WHEN status = FALSE THEN 'Seat Not Frozen'
        ELSE 'Unknown'
    END AS Freeze_Status;

END //

DELIMITER ;

3️⃣ WHILE Loop
Procedure: Display Student Preferences
DELIMITER //

CREATE PROCEDURE Show_Preferences(
    IN p_form_no CHAR(6)
)
BEGIN
    DECLARE i INT DEFAULT 1;
    DECLARE max_pref INT;

    SELECT COUNT(*) INTO max_pref
    FROM Preferences
    WHERE form_no = p_form_no;

    WHILE i <= max_pref DO
    
        SELECT *
        FROM Preferences
        WHERE form_no = p_form_no
        AND preference_no = i;

        SET i = i + 1;
        
    END WHILE;

END //

DELIMITER ;


4️⃣ REPEAT Loop
Procedure: Insert Preferences Automatically
DELIMITER //

CREATE PROCEDURE Insert_Test_Preferences(
    IN p_form_no CHAR(6)
)
BEGIN
    DECLARE i INT DEFAULT 1;

    REPEAT

        INSERT INTO Preferences
        (form_no, centre_id, course_id, preference_no)
        VALUES
        (p_form_no, 1, 1, i);

        SET i = i + 1;

    UNTIL i > 3
    END REPEAT;

END //

DELIMITER ;

5️⃣ LOOP Control Structure
Procedure: Allocate Seat Loop

DELIMITER //

CREATE PROCEDURE Allocate_Seat_Loop(
    IN p_form_no CHAR(6)
)
BEGIN
    DECLARE i INT DEFAULT 1;

    myloop: LOOP

        IF i > 3 THEN
            LEAVE myloop;
        END IF;

        INSERT INTO Seat_Allocation
        (form_no, course_id, centre_id, round_no)
        VALUES
        (p_form_no, 1, 1, i);

        SET i = i + 1;

    END LOOP;

END //

DELIMITER ;

6️⃣ Stored Procedure with INOUT Parameter
DELIMITER //

CREATE PROCEDURE Increase_Rank(
    INOUT p_rank INT
)
BEGIN

    SET p_rank = p_rank + 10;

END //

DELIMITER ;
<img width="568" height="300" alt="image" src="https://github.com/user-attachments/assets/54f713d7-bebd-4afe-b571-8984bf93f019" />

7️⃣ Cursor Example
Procedure: Display All Preferences of Students

DELIMITER //

CREATE PROCEDURE List_All_Preferences()
BEGIN

    DECLARE done INT DEFAULT FALSE;
    DECLARE f CHAR(6);
    DECLARE p INT;

    DECLARE pref_cursor CURSOR FOR
        SELECT form_no, preference_no
        FROM Preferences;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    OPEN pref_cursor;

    read_loop: LOOP

        FETCH pref_cursor INTO f, p;

        IF done THEN
            LEAVE read_loop;
        END IF;

        SELECT f AS Form_No, p AS Preference_No;

    END LOOP;

    CLOSE pref_cursor;

END //

DELIMITER ;

8️⃣ Error Handling Procedure
Example: Insert Student Safely
DELIMITER //

CREATE PROCEDURE Add_Student(
    IN p_form_no CHAR(6),
    IN p_name VARCHAR(30),
    IN p_rank INT
)
BEGIN

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        SELECT 'Error occurred while inserting student' AS Message;
    END;

    INSERT INTO CCAT_Result
    VALUES(p_form_no, p_name, p_rank);

    SELECT 'Student inserted successfully' AS Message;

END //

DELIMITER ;

These procedures cover all 4 questions in your assignment.
