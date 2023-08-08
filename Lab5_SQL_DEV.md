# Lab: Connecting to Oracle Database and Validating Prior Labs using SQL Developer

## Objective

In this lab, we will connect to the Oracle Database using SQL Developer and validate the work done in the previous labs. SQL Developer is a graphical tool that enhances productivity and simplifies database development tasks.

## Prerequisites

- Oracle SQL Developer installed on your local machine. If you don't have it installed, you can download it from the [official Oracle website](https://www.oracle.com/tools/downloads/sqldev-downloads.html).
- Access to the Oracle Database server, including the server name (or IP address), port, and necessary credentials.

## Steps

1. **Open SQL Developer:** You can do this by finding SQL Developer in your applications menu or list of installed programs, depending on your operating system.

2. **Add a new connection:** Click on the green plus (+) button or go to `File -> New -> Database Connection`.

3. **Enter the connection details:** In the New / Select Database Connection window, enter the following details (this may already exist and if it does - use the SYS connection):
    - **Connection Name:** Enter a name for this connection. You can choose any name that makes sense to you.
    - **Username:** Enter the username for your Oracle Database. In this case, we will use the `SYS` user.
    - **Password:** Enter the password for your Oracle Database. In this case, the password is `fenago`. Remember to check the `Save password` box if you don't want to enter the password every time you connect.
    - **Hostname:** Enter the hostname or IP address of your Oracle Database server.
    - **Port:** Enter the port number on which your Oracle Database is listening. The default port for Oracle Database is `1521`.
    - **SID:** Enter the SID of your Oracle Database. This is usually the name of the database instance.

    Click on the `Test` button to check the connection. If everything is set up correctly, you should see a `Success` message.

4. **Save and connect:** Click on the `Connect` button to connect to the Oracle Database.

5. **Validate the previous labs:** Once connected, you can run SQL commands to validate the work done in the previous labs. For example, to validate the creation of XMLType tables and columns, you could run the following commands:

    ```sql
    DESC mytable1;
    DESC mytable2;
    ```

    Each of these commands should display the structure of the corresponding table, confirming that the tables were created successfully. 

    Additionally, you can navigate to the "Tables" view to confirm the existence of the tables. This can be found in the "Connections" tab, under your connection -> "Schemas" -> "SYS" -> "Tables". The tables `mytable1` and `library` should be listed there.

6. **Disconnect and close SQL Developer:** Once you've finished, remember to disconnect from the Oracle Database by right-clicking on the connection and selecting `Disconnect`. You can close SQL Developer by going to `File -> Exit`.

> **Note:** You need to have the necessary permissions to connect to the Oracle Database and run these commands. If you're not the Oracle system administrator, you may need to ask them for help.
