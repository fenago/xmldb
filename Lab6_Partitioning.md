# Lab: Partitioning Tables That Contain XMLType Data Stored as Binary XML

## Objective

In this lab, we will learn how to partition tables that contain XMLType data stored as binary XML. Partitioning can greatly improve the performance of queries on large tables by dividing the data into smaller, more manageable pieces, called partitions.

## Prerequisites

- Oracle SQL Developer installed on your local machine.
- Access to the Oracle Database server, including the server name (or IP address), port, and necessary credentials.
- Basic knowledge of SQL and database partitioning concepts.

## Steps

1. **Open SQLPlus or SQL Developer:** You can open SQLPlus in a terminal or SSH session, or open SQL Developer on your local machine, depending on your preference.

2. **Connect to the Oracle Database:** If you're using SQLPlus, you can connect directly from the terminal with the following command:

    ```bash
    sqlplus / as sysdba
    ```
   
    If you're using SQL Developer, create a new connection or use an existing one to connect to the database.

3. **Create a relational table with an XMLType column:** The following SQL command creates a relational table named `reltab` with a primary key column `key_col` and an XMLType column `xml_col`. The table is partitioned by range on the `key_col`:

    ```sql
    CREATE TABLE reltab (
      key_col VARCHAR2(10) PRIMARY KEY,
      xml_col XMLType
    )
    XMLTYPE xml_col STORE AS BINARY XML
    PARTITION BY RANGE (key_col)
    (
      PARTITION P1 VALUES LESS THAN ('abc'),
      PARTITION P2 VALUES LESS THAN (MAXVALUE)
    );
    ```

    Run this command in the SQLPlus prompt or in a SQL Developer query window.

4. **Create an XMLType table with a virtual column:** The following SQL command creates an XMLType table named `po_binaryxml` with a virtual column `date_col`. The virtual column targets the `orderDate` attribute of the `PurchaseOrder` element in an XML document stored in the table. The table is partitioned by range on the `date_col`:

    ```sql
    CREATE TABLE po_binaryxml OF XMLType
    XMLTYPE STORE AS BINARY XML
    VIRTUAL COLUMNS
    (
      date_col AS (XMLCast(XMLQuery('/PurchaseOrder/@orderDate' PASSING OBJECT_VALUE RETURNING CONTENT) AS DATE))
    )
    PARTITION BY RANGE (date_col)
    (
      PARTITION orders2001 VALUES LESS THAN (to_date('01-JAN-2002')),
      PARTITION orders2002 VALUES LESS THAN (MAXVALUE)
    );
    ```

    Run this command in the SQLPlus prompt or in a SQL Developer query window.

5. **Validate the table creation:** You can validate the creation of the tables and their partitions by describing the tables:

    ```sql
    DESC reltab;
    DESC po_binaryxml;
    ```

    These commands should display the structures of the `reltab` and `po_binaryxml` tables, including their partitions, confirming that they were created successfully.

6. **Disconnect from the Oracle Database:** Once you've finished, remember to disconnect from the Oracle Database. In SQLPlus, you can do this with the `exit` command. In SQL Developer, you can right-click on the connection and select `Disconnect`.

## Challenge Exercise

Now that you've learned how to create partitioned tables with XMLType data, it's time to apply what you've learned. Your task is to create a new XMLType table named `orders` that stores XML documents representing customer orders. Each order document has an `orderDate` attribute on the root element, and you're interested in partitioning the table based on the year of this date.

You'll need to:

- Create a virtual column that extracts the year from the `orderDate` attribute.
- Partition the table by range on the virtual column.
- Create at least two partitions: one for orders made in 2022 and earlier, and another for orders made in 2023 and later.

Remember, you can use either SQLPlus or SQL Developer for this task. Good luck!

> **Note:** You need to have the necessary permissions to connect to the Oracle Database and run these commands. If you're not the Oracle system administrator, you may need to ask them for help.
