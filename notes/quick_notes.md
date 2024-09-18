## Copy Data
- On Error: we can use ON_ERROR in copy command with various options
  - SKIP_FILE: file with error records will be skipped
  - SKIP_FILE_<error_threshold>: file will skipped if having more error records  than specified in threshold
  - ABORT_STATEMENT : is default action, will terminate copy if error occured
  - CONTINUE: will kepp loading dat in case of error
- FILE FORMAT objet: Like staging object we can also create an object for file format and reuse it in COPY command
  - Create schema : CREATE OR REPLACE SCHEMA MANAGE_DB.file_format;
  - Create format object: CREATE OR REPLACE file format  MANAGE_DB.file_format.my_file_format;
 ## Copy Options
 - - Validation Mode: while copying dat we can use this mode just to validate data it will nor load the data. below are the different types.
 -   - validation_mode=return_errors : this option will show error from entire file
     - validation_mode=return_rows_N : this will validate data of N rows and will show the data
   - Rejected records: we can chec the rejected records
     - we can get rejected data from table(result_scan(





