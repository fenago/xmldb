# Lab: Creating XMLType Tables and Columns in Oracle Database

## Objective:
In this lab, we will create tables with XMLType columns in an Oracle Database. XMLType is a system-defined opaque type for handling XML data. It has predefined member functions to extract XML nodes and fragments.

## Steps:

1. **Open a terminal:** You can SSH into the server or open a terminal if you have physical access to the machine.

2. **Switch to the Oracle user:** Oracle installations are usually owned by the "oracle" user. Switch to this user with the following command:
    ```bash
    su - oracle
    ```

3. **Set up the Oracle environment:** Before you can run any Oracle commands, you need to set up the Oracle environment. This is usually done by running a script that was created during the Oracle installation. This script is usually located in the Oracle user's home directory and is named something like `setOraEnv.sh` or `oraenv`. You can source this script with the following command:
    ```bash
    source ~/setOraEnv.sh
    ```
    or
    ```bash
    . oraenv
    ```

4. **Create a table with an XMLType column:** Connect to your database as SYSDBA and create a table named `mytable1` with an XMLType column named `xml_column` and a primary key named `key_column` with the following commands:
    ```bash
    sqlplus / as sysdba
    ```
    Once you're in the SQL*Plus prompt, run the following command:
    ```sql
    CREATE TABLE mytable1 (key_column VARCHAR2(10) PRIMARY KEY, xml_column XMLType);
    ```

5. **Create a table of XMLType:** Still in the SQL*Plus prompt, create a table named `mytable2` of XMLType with the following command:
    ```sql
    CREATE TABLE mytable2 OF XMLType;
    ```

6. **Create a table based on a use case:** For example, let's consider a use case where we are storing XML data for different books in a library. The `book_id` will be our primary key and the `book_data` will be an XMLType column containing all the book details. Run the following command:
    ```sql
    CREATE TABLE library (book_id VARCHAR2(10) PRIMARY KEY, book_data XMLType);
    ```

7. **Validation step:** To ensure that the tables have been created successfully, we can describe the tables and check their structures. Run the following commands:
    ```sql
    DESCRIBE mytable1;
    DESCRIBE mytable2;
    DESCRIBE library;
    ```
    These commands should display the structures of `mytable1`, `mytable2`, and `library`, confirming that they were created successfully.

8. **Exit SQL*Plus:** Once you've finished with SQL*Plus, you can exit with the following command:
    ```sql
    exit
    ```

> **Note:** You need to have the necessary permissions to perform these actions. If you're not the Oracle system administrator, you may need to ask them for help.
