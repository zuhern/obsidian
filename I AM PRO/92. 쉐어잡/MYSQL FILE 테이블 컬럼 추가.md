---
Created: Invalid date
Updated: Invalid date
---
ALTER TABLE CTN_FILES ADD COLUMN `FILE_FOR` varchar(10) NOT NULL DEFAULT '' COMMENT '파일사용영역';

CREATE TABLE `CTN_FILES_TMP` (

`FILE_ID` char(12) NOT NULL COMMENT '파일ID',

`PARENT_ID` varchar(20) NOT NULL DEFAULT '' COMMENT '파일의부모ID',

`FILE_INDEX` decimal(10,0) NOT NULL COMMENT '순서',

`FILE_TYPE` varchar(10) DEFAULT NULL COMMENT '파일타입',

`FILE_NM` varchar(200) DEFAULT NULL COMMENT '파일명',

`URL` varchar(200) DEFAULT NULL COMMENT 'URL',

`DELETED_YN` enum('N','Y') DEFAULT 'N' COMMENT '삭제여부',

`REG_ACC_ID` char(12) DEFAULT NULL COMMENT '등록계정ID',

`LAST_MOD_DATE` datetime(3) NOT NULL ON UPDATE CURRENT_TIMESTAMP(3) COMMENT '최종수정일자',

`REG_DATE` datetime(3) NOT NULL COMMENT '등록일자',

`FILE_DIV` char(3) DEFAULT NULL COMMENT '파일구분',

`FILE_FOR` varchar(10) NOT NULL DEFAULT '' COMMENT '파일사용영역',

PRIMARY KEY (`FILE_ID`,`PARENT_ID`,`FILE_INDEX`,`FILE_FOR`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='파일';

INSERT INTO CTN_FILES_TMP

SELECT * FROM CTN_FILES;

UPDATE CTN_FILES AS T2

SET T2.FILE_FOR = (

SELECT SUBSTRING_INDEX(URL, '/', 1)

FROM CTN_FILES_TMP AS T1

WHERE T1.FILE_ID = T2.FILE_ID

);

ALTER TABLE CTN_FILES DROP PRIMARY KEY;

ALTER TABLE CTN_FILES ADD PRIMARY KEY (FILE_ID, PARENT_ID, FILE_INDEX, FILE_FOR);