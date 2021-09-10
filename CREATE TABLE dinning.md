CREATE TABLE `dinning`.`orders` (`o_id` serial,`a_id` INT,`d_id` INT,`date_in` TIMESTAMP,`date_out` TIMESTAMP,`o_income` DOUBLE,`o_state` SMALLINT);

CREATE TABLE `dinning`.`CUISINE` (`c_id` serial,`c_name` VARCHAR(255),`c_cost` DOUBLE,`c_price` DOUBLE,`c_img` VARCHAR(255),`c_info` VARCHAR(255),`c_type` SMALLINT,`c_exist` SMALLINT);

