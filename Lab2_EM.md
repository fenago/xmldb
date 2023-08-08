# Lab: Starting Oracle EM Express and Logging In on CentOS 7 with Oracle 19c

## Objective:
In this lab, we will start Oracle Enterprise Manager (EM) Express on a CentOS 7 server with Oracle 19c, and then log in to EM Express using specific credentials.

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

4. **Set the EM Express HTTPS port:** Connect to your database as SYSDBA and set the HTTPS port for EM Express with the following commands:
    ```bash
    sqlplus / as sysdba
    ```
    Once you're in the SQL*Plus prompt, run the following command:
    ```sql
    EXEC DBMS_XDB_CONFIG.SETHTTPSPORT(5500);
    ```
    This command sets the HTTPS port for EM Express to 5500. You can choose a different port if you like, but remember that port numbers below 1024 are considered "privileged" on Unix-like systems, and only root can bind to them.

5. **Verify the configuration:** You can verify that EM Express is now configured to listen on the port you set by running the following command in SQL*Plus:
    ```sql
    SELECT DBMS_XDB_CONFIG.GETHTTPSPORT() FROM dual;
    ```
    The output of this command should now be 5500, the port number you set in the previous step.

6. **Exit SQL*Plus:** Once you've finished with SQL*Plus, you can exit with the following command:
    ```sql
    exit
    ```

7. **Access EM Express:** Once EM Express is configured, you can access it by opening a web browser and navigating to `https://<hostname>:5500/em`, replacing `<hostname>` with the hostname or IP address of your Oracle server.

8. **Log in to EM Express:** You can log in to EM Express using the following credentials:
    - **Username:** sys
    - **Password:** fenago
    - **Container:** LEAVE_BLANK or use 'CDB$ROOT' as you are connecting to the root container of a CDB.

> **Note:** You need to have the necessary permissions to perform these actions. If you're not the Oracle system administrator, you may need to ask them for help.
