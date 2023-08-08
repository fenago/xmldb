## How to Check Configured Oracle Databases on CentOS 7 with Oracle 19c

1. **Open a terminal:** This can be done via SSH into the server or directly if you have physical access to the machine.

2. **Switch to the Oracle user:** Oracle installations are usually owned by the "oracle" user. Switch to the oracle user with the following command:
    ```bash
    su - oracle
    ```

3. **Set up the Oracle environment:** You need to set up the Oracle environment before running any Oracle commands. This is usually done by running a script created during the Oracle installation. This script is usually located in the oracle user's home directory and can have names like `setOraEnv.sh` or `oraenv`. You can source this script with the following command:
    ```bash
    source ~/setOraEnv.sh
    ```
    or
    ```bash
    . oraenv
    ```

4. **Check the Oracle databases:** After the environment setup, you can run the following command to check the status of the Oracle listener. This command will display a list of services, which includes the Oracle databases currently configured and running.
    ```bash
    lsnrctl status
    ```
    If you're looking for specific databases, you can also query the `v$database` view in SQL*Plus to get information about the database currently connected to. This can be done with the following command:
    ```bash
    sqlplus / as sysdba
    ```
    Once you're in the SQL*Plus prompt, run the following command:
    ```sql
    SELECT name FROM v$database;
    ```
    This will give you the name of the database that SQL*Plus is currently connected to.

> **Note:** You need to have the necessary permissions to perform these actions. If you're not the Oracle system administrator, you may need to ask them for help.
