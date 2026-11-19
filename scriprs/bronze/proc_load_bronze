/*
===============================================================================
Stored Procedure: Load Bronze Layer (Source -> Bronze)
===============================================================================
Script Purpose:
    This stored procedure loads data into the 'bronze' schema from external CSV files.
    It performs the following actions:
    - Truncates the bronze tables before loading data.
    - Uses the `BULK INSERT` command to load data from csv Files to bronze tables.

Parameters:
    None.
      This stored procedure does not accept any parameters or return any values.

Usage Example:
    EXEC bronze.load_bronze;

Note:
    The BULK INSERT paths point to 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets'.
    Change them to the folder where you saved the datasets.
===============================================================================
*/
CREATE OR ALTER PROCEDURE bronze.load_bronze AS 
BEGIN
	DECLARE @start_time DATETIME ,@end_time DATETIME ,@process_start_time DATETIME ,@process_end_time DATETIME
		BEGIN TRY
			SET @process_start_time= GETDATE();
			-- Truncating table 
			PRINT'===============================================================';
			PRINT'Loading bronze layer';
			PRINT'===============================================================';
			PRINT'---------------------------------------------------------------';
			PRINT'Loading CRM tables ';
			PRINT'---------------------------------------------------------------';
			PRINT'>> Truncating Table : bronze.crm_cust_info';
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.crm_cust_info;
			PRINT'<<Iserting data into table :bronze.crm_cust_info ';
			-- insert data into table
			BULK INSERT bronze.crm_cust_info
			from 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_crm\cust_info.csv'
				WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.crm_cust_info Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR)+' second';
			PRINT'--------------------------------------------------------------------------------------------------';
			PRINT'>> Truncating Table : bronze.crm_prd_info';
			-- Truncating table 
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.crm_prd_info;
			PRINT'<<Inserting data into table : bronze.crm_prd_info';
			-- insert data into table
			BULK INSERT bronze.crm_prd_info
			FROM 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_crm\prd_info.csv'
			WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.crm_prd_info Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR) + ' secound' ;
			PRINT'--------------------------------------------------------------------------------------------------';
			PRINT'>> Truncating Table : bronze.crm_sales_details';
			-- Truncating table
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.crm_sales_details;
			PRINT'<<Iserting data into table : bronze.crm_sales_details';
			-- insert data into table
			BULK INSERT bronze.crm_sales_details
			FROM 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_crm\sales_details.csv'
			WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.crm_sales_details Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR) + ' secound';
			PRINT'---------------------------------------------------------------';
			PRINT'Loading ERP tables';
			PRINT'---------------------------------------------------------------';
			PRINT'>> Truncating Table : bronze.erp_cust_az12';
			-- Truncating table
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.erp_cust_az12;
			-- insert data into table
			PRINT'<<Iserting data into table : bronze.erp_cust_az12';
			BULK INSERT bronze.erp_cust_az12
			FROM 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_erp\CUST_AZ12.csv'
			WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.erp_cust_az12 Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR) + ' secound';
			PRINT'--------------------------------------------------------------------------------------------------'
			PRINT'>> Truncating Table : bronze.erp_loc_a101';
			-- Truncating table
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.erp_loc_a101;
			PRINT'<<Iserting data into table : bronze.erp_loc_a101';
			-- insert data into table
			BULK INSERT bronze.erp_loc_a101
			FROM 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_erp\LOC_A101.csv'
			WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.erp_loc_a101 Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR) + ' secound';
			PRINT'--------------------------------------------------------------------------------------------------'
			PRINT'>> Truncating Table : bronze.erp_px_cat_g1v2';
			-- Truncating table
			SET @start_time = GETDATE();
			TRUNCATE TABLE bronze.erp_px_cat_g1v2;
			PRINT'<<Iserting data into table : bronze.erp_px_cat_g1v2';
			-- insert data into table
			BULK INSERT bronze.erp_px_cat_g1v2
			FROM 'D:\SQL Braa\sql-data-warehouse-project-main\01_datasets\source_erp\PX_CAT_G1V2.csv'
			WITH(
					FIRSTROW = 2 ,
					FIELDTERMINATOR =',',
					TABLOCK
			);
			SET @end_time = GETDATE();
			PRINT 'bronze.erp_px_cat_g1v2 Load Duration : ' +CAST(DATEDIFF(SECOND,@start_time,@end_time) AS NVARCHAR) + ' secound';
			PRINT'--------------------------------------------------------------------------------------------------'
			SET @process_end_time = GETDATE();
			PRINT'==================================================================';
			PRINT'Bronze Layer Liading is Completed';
			PRINT'Loading Duration : ' + CAST(DATEDIFF(SECOND,@process_start_time,@process_end_time) AS NVARCHAR) + ' secound';
			PRINT'==================================================================';
		END TRY 
	BEGIN CATCH
		PRINT'==================================================================';
		PRINT'AN ERROR OCCURED';
		PRINT'ERROR MESSAGE'+ERROR_MESSAGE();
		PRINT'ERROR NUMBER:'+CAST(ERROR_NUMBER() AS NVARCHAR);
		PRINT'ERROR State:'+CAST(ERROR_STATE() AS NVARCHAR);
		PRINT'ERROR LINE:'+CAST(ERROR_LINE() AS NVARCHAR);
		PRINT'==================================================================';
	END CATCH 
END
