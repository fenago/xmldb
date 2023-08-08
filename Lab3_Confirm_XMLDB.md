# Lab: Getting Started with Oracle XML DB

## Objective:
In this lab, we will check if Oracle XML DB is installed on our system. Oracle XML DB is a high-performance, native XML storage and retrieval technology that is delivered as a part of all versions of Oracle Database. If it's installed, we will have access to the database schema (user account) XDB and the view `RESOURCE_VIEW`.

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

4. **Check if the XDB user exists:** Connect to your database as SYSDBA and check the existence of the XDB user with the following commands:
    ```bash
    sqlplus / as sysdba
    ```
    Once you're in the SQL*Plus prompt, run the following command:
    ```sql
    SELECT username FROM all_users WHERE username = 'XDB';
    ```
    If Oracle XML DB is installed, this will return 'XDB'. If the query doesn't return anything, it means that Oracle XML DB is not installed.

5. **Check if the RESOURCE_VIEW view exists:** Still in the SQL*Plus prompt, check the existence of the `RESOURCE_VIEW` view with the following command:
    ```sql
    SELECT * FROM all_objects WHERE object_type = 'VIEW' AND object_name = 'RESOURCE_VIEW';
    ```
    If Oracle XML DB is installed, this will return information about the `RESOURCE_VIEW` view. If the query doesn't return anything, it means that the `RESOURCE_VIEW` view does not exist, indicating that Oracle XML DB is not installed.

6. **Exit SQL*Plus:** Once you've finished with SQL*Plus, you can exit with the following command:
    ```sql
    exit
    ```

> **Note:** You need to have the necessary permissions to perform these actions. If you're not the Oracle system administrator, you may need to ask them for help.
