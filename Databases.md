---
created: 2021-08-30T08:22:56+02:00
modified: 2021-08-30T08:23:54+02:00
---

# Databases for modelbuilderapplication

# Modelbuilder database
[TOC]
* * *
## Structure

```
[DB]: modelbbuilder
├─┬─[TBL]: category
│ └─┬─[REC]: category_Id			int 		NOT NULL	**PK**
│   ├─[REC]: category_Description		varchar(255)
│   └─[REC]: category_ParentId			int
│
├─┬─[TBL]: countries
│ └─┬─[REC]: country_Id				int 		NOT NULL	**PK**
│   ├─[REC]: country_code			varchar(4)			**UK** 
│   ├─[REC]: currency_Symbol			varchar(2)
│   ├─[REC]: country_Description		varchar(45)
│   └─[REC]: currency_Id 			int
│
├─┬─[TBL]: currencies
│ └─┬─[REC]: currency_Id			int		NOT NULL	**PK**
│   ├─[REC]: currency_Code			varchar(4)	NOT NULL	**UK**
│   ├─[REC]: currency_Symbol 			varchar(2) 	NOT NULL	**UK**
│   ├─[REC]: currency_Description		varchar(45)	NOT NULL
│   └─[REC]: currency_ConversionRate		float
│
├─┬─[TBL]: language
│ └─┬─[REC]: language_Id			int		NOT NULL	**PK**
│   ├─[REC]: language_code 			varchar(4)	NOT NULL	**UK**
│   └─[REC]: language_Description		varchar(45)	NOT NULL
│
├─┬─[TBL]: products
│ └─┬─[REC]: product_Id				int		NOT NULL	**PK**
│   ├─[REC]: product_Code			varchar(20) 	NOT NULL	**UK**
│   ├─[REC]: product_Description		varchar(150) 	NOT NULL
│   ├─[REC]: category_Id			int
│   ├─[REC]: category_Description 		varchar(45)
│   ├─[REC]: supplier_Id 			int
│   ├─[REC]: supplier_Name 			varchar(45)
│   ├─[REC]: product_SupplierProductNumber	varchar(20)
│   ├─[REC]: storage_Id 			int
│   ├─[REC]: storage_Description 		varchar(50)
│   └─[REC]: product_Price 			float
│
├─┬─[TBL]: projects
│ └─┬─[REC]: projects_Id			int		NOT NULL	**PK**
│   ├─[REC]: projects_Description		varchar(50)	NOT NULL
│   ├─[REC]: projects_StartDate			date
│   ├─[REC]: projects_ExpectedEndDate		date
│   ├─[REC]: projects_EndDate			date
│   ├─[REC]: projects_TotalCost			decimal(5,2)
│   └─[REC]: projects_TotalMinutes		int
│
├─┬─[TBL]: storage
│ └─┬─[REC]: storage_Id				int		NOT NULL	**PK**
│   ├─[REC]: storage_Code			varchar(20)	NOT NULL	**UK**
│   └─[REC]: storage_Description		varchar(150)	
│
├─┬─[TBL]: supplier
│ └─┬─[REC]: supplier_Id			int		NOT NULL	**PK**
│   ├─[REC]: supplier_Code			varchar(20) 	NOT NULL	**UK**
│   ├─[REC]: supplier_Name			varchar(150) 	NOT NULL
│   ├─[REC]: supplier_Address1			varchar(150)
│   ├─[REC]: supplier_Address2			varchar(150)
│   ├─[REC]: supplier_Zip			varchar(15)
│   ├─[REC]: supplier_City			varchar(40)
│   ├─[REC]: country_Id				int
│   ├─[REC]: country_Code			varchar(4)
│   ├─[REC]: supplier_Url			varchar(255)
│   ├─[REC]: supplier_PhoneGeneral		varchar(40)
│   ├─[REC]: supplier_PhoneSales		varchar(40)
│   ├─[REC]: supplier_PhoneSupport		varchar(40)
│   ├─[REC]: supplier_MailGeneral		varchar(80)
│   ├─[REC]: supplier_MailSales			varchar(80)
│   ├─[REC]: supplier_MailSupport		varchar(80)
│   ├─[REC]: supplier_Memo			longtext
│   ├─[REC]: currency_Id			int
│   └─[REC]: currency_Code			varchar(4)
│
└─┬─[TBL]: worktypes
  └─┬─[REC]: worktypes_Id			int		NOT NULL	**PK**
    ├─[REC]: worktypes_Description		varchar(45)
    └─[REC]: worktypes_ParentId			int
```

# Scripts to create database or datatables
## Database
```SQL
CREATE DATABASE IF NOT EXISTS `modelbuilder` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */;
USE `modelbuilder`;
```
## Category datatable
```SQL
CREATE TABLE IF NOT EXISTS `category` (
  `category_Id` int NOT NULL AUTO_INCREMENT,
  `category_Description` varchar(45) DEFAULT NULL,
  `category_ParentId` int DEFAULT NULL,
  PRIMARY KEY (`category_Id`)
)ENGINE=InnoDB AUTO_INCREMENT=490 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```


## Country datatable
```SQL
CREATE TABLE IF NOT EXISTS `countries` (
  `country_Id` int NOT NULL AUTO_INCREMENT,
  `country_Code` varchar(4) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL,
  `currency_Symbol` varchar(2) NOT NULL DEFAULT '€',
  `country_Description` varchar(45) DEFAULT NULL,
  `currency_Id` int DEFAULT '1',
  PRIMARY KEY (`country_Id`),
  UNIQUE KEY `country_code_UNIQUE` (`country_Code`)
) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

### Country Data
```SQL
INSERT INTO `countries` (`country_Id`, `currency_Symbol`, `country_Code`, `country_Description`, `currency_Id`) VALUES
	(1, '€', 'NL', 'Nederland', 1),
	(2, '£', 'UK', 'United Kingdom', 2),
	(3, '$', 'US', 'United States', 3),
	(4, '€', 'DE', 'Duitsland', 1);
```

## Currency Datatable
```SQL
CREATE TABLE IF NOT EXISTS `currencies` (
  `currency_Id` int NOT NULL AUTO_INCREMENT,
  `currency_Code` varchar(4) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL DEFAULT 'EUR',
  `currency_Symbol` varchar(2) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL DEFAULT '€',
  `currency_Description` varchar(45) NOT NULL,
  `currency_ConversionRate` float DEFAULT NULL,
  PRIMARY KEY (`currency_Id`),
  UNIQUE KEY `currency_Code` (`currency_Code`),
  UNIQUE KEY `currency_Symbol` (`currency_Symbol`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

### Currency Data
```SQL
INSERT INTO `currencies` (`currency_Id`, `currency_Code`, `currency_Symbol`, `currency_Description`, `currency_ConversionRate`) VALUES
	(1, 'EUR', '€', 'Euro', 1.0000),
	(2, 'GBP', '£', 'Britse pond', 1.1079),
	(3, 'USD', '$', 'Amerikaanse dollar', 0.8442);
```

## Language Datatable
```SQL
CREATE TABLE `language` (
	`language_Id` INT(10) NOT NULL AUTO_INCREMENT,
	`language_code` VARCHAR(4) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`language_Description` VARCHAR(45) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	PRIMARY KEY (`language_Id`) USING BTREE,
	UNIQUE INDEX `language_code` (`language_code`) USING BTREE
)
COLLATE='utf8mb4_0900_ai_ci'
ENGINE=InnoDB
;
```

### Language Data
```SQL
INSERT INTO `language` (`language_Id`, `language_Description`) VALUES
	(1, 'NL', 'Nederlands'),
	(2, 'EN', 'English'),
	(3, 'DE', 'Deutsch');
```

## Products Datatable
```SQL
CREATE TABLE `products` (
	`product_Id` INT(10) NOT NULL AUTO_INCREMENT,
	`product_Code` VARCHAR(20) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`product_Description` VARCHAR(150) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`category_Id` INT(10) NULL DEFAULT NULL,
	`category_Description` VARCHAR(45) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Id` INT(10) NULL DEFAULT NULL,
	`supplier_Name` VARCHAR(45) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`product_SupplierProductNumber` VARCHAR(20) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`storage_Id` INT(10) NULL DEFAULT NULL,
	`storage_Description` VARCHAR(50) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`product_Price` FLOAT NULL DEFAULT NULL,
	PRIMARY KEY (`product_Id`) USING BTREE,
	UNIQUE INDEX `product_Code` (`product_Code`) USING BTREE
)
COLLATE='utf8mb4_0900_ai_ci'
ENGINE=InnoDB
;
```

## Projects Datatable
```SQL
CREATE TABLE IF NOT EXISTS `projects` (
  `projects_Id` int NOT NULL AUTO_INCREMENT,
  `projects_Description` varchar(50) NOT NULL,
  `projects_StartDate` date DEFAULT NULL,
  `projects_ExpectedEndDate` date DEFAULT NULL,
  `projects_EndDate` date DEFAULT NULL,
  `projects_TotalCost` decimal(5,2) DEFAULT NULL,
  `projects_TotalMinutes` int DEFAULT NULL,
  PRIMARY KEY (`projects_Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

## Storage Datatable
```SQL
CREATE TABLE `storage` (
	`storage_Id` INT(10) NOT NULL AUTO_INCREMENT,
	`storage_Code` VARCHAR(20) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`storage_Description` VARCHAR(150) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	PRIMARY KEY (`storage_Id`) USING BTREE,
	UNIQUE INDEX `storage_Code` (`storage_Code`) USING BTREE50) NOT NULL,
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

## Supplier Datatable
```SQL
CREATE TABLE `supplier` (
	`supplier_Id` int(10) NOT NULL AUTO_INCREMENT,
	`supplier_Code` varchar(20) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Name` varchar(150) NOT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Address1` varchar(150) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Address2` varchar(150) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Zip` varchar(15) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_City` varchar(40) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`country_Id` int(10) NULL DEFAULT NULL,
	`country_Code` varchar(4) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Url` varchar(255) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_PhoneGeneral` varchar(40) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_PhoneSales` varchar(40) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_PhoneSupport` varchar(40) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_MailGeneral` varchar(80) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_MailSales` varchar(80) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_MailSupport` varchar(80) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`supplier_Memo` longtext NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`currency_Id` int(10) NULL DEFAULT NULL,
	`currency_Code` varchar(4) NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	PRIMARY KEY (`supplier_Id`) USING BTREE,
	UNIQUE INDEX `supplier_Code` (`supplier_Code`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

## Worktypes Datatable
```SQL
CREATE TABLE IF NOT EXISTS `worktypes` (
  `worktypes_Id` int NOT NULL AUTO_INCREMENT,
  `worktypes_Description` varchar(45) DEFAULT NULL,
  `worktypes_ParentId` int DEFAULT NULL,
  PRIMARY KEY (`worktypes_Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
