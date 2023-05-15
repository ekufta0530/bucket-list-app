# Setting up the database

'mysql -u <username> -p`

`CREATE DATABASE BucketList;`

Now add the table:
```SQL
CREATE TABLE `BucketList`.`tbl_user` (
  `user_id` BIGINT NOT NULL AUTO_INCREMENT,
  `user_name` VARCHAR(45) NULL,
  `user_username` VARCHAR(45) NULL,
  `user_password` VARCHAR(45) NULL,
  PRIMARY KEY (`user_id`)
);
```

Now add the procedure

```SQL
CREATE PROCEDURE `sp_createUser`(
    IN p_name VARCHAR(20),
    IN p_username VARCHAR(20),
    IN p_password VARCHAR(20)
)
BEGIN
    DECLARE userCount INT;
    SET userCount = (SELECT COUNT(*) FROM tbl_user WHERE user_username = p_username);

    IF userCount > 0 THEN
        SELECT 'Username Exists !!';
    ELSE
        INSERT INTO tbl_user (user_name, user_username, user_password)
        VALUES (p_name, p_username, p_password);
    END IF;
END;
```