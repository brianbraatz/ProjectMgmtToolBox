---
created: 2024-03-22T13:15:49 (UTC -05:00)
tags: []
source: https://zappysys.com/api/integration-hub/jira-connector/c-sharp
author: How may I help you today?
---

# C# Jira Connector - Read/Write Jira Data in C# - Coding free API Integration | Jira API | ZappySys | SSIS | ODBC

source: https://zappysys.com/api/integration-hub/jira-connector/c-sharp

> ## Excerpt
> Read/Write Jira Data in C#. Jira Connector can be used to integrate Jira and your defined data source, e.g. Microsoft SQL, Oracle, Excel, Power BI, etc. Get, write, delete Issues, Users, Worklogs, Comments just in a few clicks!

---
<table data-dm-inline-border-top="" data-dm-inline-border-right="" data-dm-inline-border-bottom="" data-dm-inline-border-left=""><tbody><tr><td><h2>C# Jira Connector</h2><p>In this article you will learn how to integrate <text>Jira</text> data to C# (live / bi-directional connection to <text>Jira</text>). <text>Jira Connector can be used to integrate Jira and your defined data source, e.g. Microsoft SQL, Oracle, Excel, Power BI, etc. Get, write, delete Issues, Users, Worklogs, Comments just in a few clicks!</text>.</p><p>Using Jira Connector you will be able to connect, read, and write data from within C#. Follow the steps below to see how we would accomplish that.</p><p><a href="https://zappysys.com/products/odbc-powerpack/download/"><i></i>Download</a>&nbsp; <a href="https://zappysys.com/api/integration-hub/jira-connector/help/odbc-getting-started"><i></i>Help File</a>&nbsp; <a href="https://zappysys.com/products/odbc-powerpack/purchase"><i></i>Buy</a>&nbsp;</p><div id="toc_container"><p><strong>Contents</strong></p><ol><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid1" onclick="scrollToBlock('#zid1');return false;">Create ODBC Data Source (DSN) based on ZappySys API Driver</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid2" onclick="scrollToBlock('#zid2');return false;">Read data in C# from the DSN</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid3" onclick="scrollToBlock('#zid3');return false;">Insider Insights</a><ol><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid4" onclick="scrollToBlock('#zid4');return false;">While using ExecuteNonQuery make sure to use output=0.</a></li></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid5" onclick="scrollToBlock('#zid5');return false;">Create Custom Store Procedure in ZappySys Driver</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid6" onclick="scrollToBlock('#zid6');return false;">Create Custom Virtual Table in ZappySys Driver</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid7" onclick="scrollToBlock('#zid7');return false;">Conclusion</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid8" onclick="scrollToBlock('#zid8');return false;">Actions supported by Jira Connector</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid9" onclick="scrollToBlock('#zid9');return false;">Jira Connector Examples for C# Connection</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid10" onclick="scrollToBlock('#zid10');return false;">Other App Integration scenarios for Jira</a><ol></ol></li><li><a href="https://zappysys.com/api/integration-hub/jira-connector/c-sharp#zid11" onclick="scrollToBlock('#zid11');return false;">Other Connectors for C#</a><ol></ol></li></ol></div></td><td></td></tr></tbody></table>

## Create ODBC Data Source (DSN) based on ZappySys API Driver

To get data from Jira using C# we first need to create a DSN (Data Source) which will access data from Jira. We will later be able to read data using C#. Perform these steps:

1.  Install [ZappySys ODBC PowerPack](https://zappysys.com/products/odbc-powerpack/download/).
    
2.  Open ODBC Data Sources (x64):  
    ![Open ODBC Data Source](https://zappysys.com/blog/wp-content/uploads/2018/03/odbc-data-source-64-bits.png "Open ODBC Data Source")
    
3.  Create a **User Data Source** (User DSN) based on _ZappySys API Driver_
    
    ZappySys API Driver
    
    ![Create new System DSN for ZappySys API Driver](https://zappysys.com/api/images/odbc-driver-user-dsn-creation.png "Create new System DSN for ZappySys API Driver")
    
    You should create a **System DSN** (instead of a User DSN) if the client application is launched under a Windows System Account, e.g. as a Windows Service. If the client application is 32-bit (x86) running with a System DSN, use **ODBC Data Sources (32-bit)** instead of the 64-bit version.
    
4.  When the Configuration window appears give your data source a name if you haven't done that already, then select "**Jira**" from the list of _Popular Connectors_. If "Jira" is not present in the list, then click "**Search Online**" and download it. Then set the path to the location where you downloaded it. Finally, click **Continue >>** to proceed with configuring the DSN:
    
    JiraDSN
    
    Jira
    
    ![ODBC DSN Template Selection](https://zappysys.com/api/images/odbc-dsn-template-selection-walkthrough.png "ODBC DSN Template Selection")
    
5.  Now it's time to configure the Connection Manager. Select _Authentication Type_, e.g. **Token Authentication**. Then select _API Base URL_ (in most cases, the default one is the right one). More info is available in the [Authentication section](https://zappysys.com/api/integration-hub/jira-connector/help/authentication/Http).
    
    ####  [**API Key based Authentication \[Http\]**](https://zappysys.com/api/integration-hub/jira-connector/c-sharp#collapse_0fe3b7fa-a537-4e2f-8874-239ae6f3ea0c1)
    
    **Steps to get Jira Credentials**  
    Firstly, login into your Atlassian account and then go to your Jira profile:
    
    1.  Go to [Profile > Security](https://id.atlassian.com/manage-profile/security).
    2.  Click [Create and manage API tokens](https://id.atlassian.com/manage-profile/security/api-tokens).
    3.  Then click **Create API token** button and give your token a label.
    4.  When window appears with new API token, copy and use it in this connection manager.
    5.  That's it!
    
    Fill in all required parameters and set optional parameters if needed:
    
    JiraDSN
    
    Jira
    
    API Key based Authentication \[Http\]
    
    https://\[$Subdomain$\].atlassian.net/rest/api/3
    
    ![ODBC DSN HTTP Connection Configuration](https://zappysys.com/api/images/odbc-dsn-connection-configuration-walkthrough.png "ODBC DSN HTTP Connection Configuration")
    
6.  Once the data source has been configured, you can preview data. Select the **Preview** tab and use settings similar to the following to preview data:  
    ![ODBC ZappySys Data Source Preview](https://zappysys.com/api/images/odbc-data-source-preview.png "ODBC ZappySys Data Source Preview")
    
7.  Click **OK** to finish creating the data source.
    

## Read data in C# from the DSN

1.  Create a new Console project and use this code to read the data:  
    
    "JiraDSN";
    
    ![Make ZappySys Driver call in c#](https://zappysys.com/api/images/csharp/01-csharp-load-data-from-api-provider-via-odbc.png "Make ZappySys Driver call in c#")
    
2.  Press F5 to run the code and read the data:  
    ![ZappySys Driver Output in c#](https://zappysys.com/api/images/csharp/02-csharp-load-data-from-api-connector-via-odbc-data-results.png "ZappySys Driver Output in c#")
    
3.  Here is the code in text format:
    
    ```
    
    <span><span><span>using</span></span></span> System;
    <span><span><span>using</span></span></span> System.Data.Odbc;
    
    <span><span><span>namespace</span></span></span> <span><span><span>ConsoleApp</span></span></span> {
        <span><span><span>class</span></span></span> <span><span><span>Program</span></span></span> {
            <span><span><span><span><span><span>static</span></span></span></span></span><span><span> </span></span><span><span><span><span><span>void</span></span></span></span></span><span><span> </span></span><span><span><span><span><span>Main</span></span></span></span></span><span><span>(</span></span><span></span><span><span></span><span><span></span>) </span></span></span>{
                <span><span><span>var</span></span></span> dsn = <span><span><span>"JiraDSN"</span></span></span>;
                <span><span><span>using</span></span></span> (<span><span><span>var</span></span></span> conn = <span><span><span>new</span></span></span> OdbcConnection(String.Format(<span><span><span>"DSN={0}"</span></span></span>, dsn)))
                {
                    conn.Open();
                    <span><span><span>var</span></span></span> cmd = <span><span><span>new</span></span></span> OdbcCommand(<span><span><span>"SELECT * FROM Products"</span></span></span>, conn);
                    
                    <span><span><span>//Increase the timeout duration from the default 30 seconds, which may be insufficient in certain scenarios</span></span></span>
                    cmd.CommandTimeout=<span><span><span>600</span></span></span>; <span><span><span>// 600-Seconds</span></span></span>
                    
                    <span><span><span>var</span></span></span> rdr = cmd.ExecuteReader();
                    <span><span><span>while</span></span></span> (rdr.Read())
                    {
                        <span><span><span>for</span></span></span> (<span><span><span>int</span></span></span> i = <span><span><span>0</span></span></span>; i &lt; rdr.FieldCount; i++)
                        {
                                Console.Write(<span><span><span>"{0}\t"</span></span></span>, rdr[i]);
                        }
                        Console.WriteLine();
                    }
                }
                Console.ReadKey();
            }
        }
    }
    ```
    
4.  If you want to avoid being dependent on a DSN and creating multiple DSNs for each platform (x86, x64), then you can use a fully qualified connection string. [Simply go to your DSN and copy the Connection String](https://zappysys.zendesk.com/hc/en-us/articles/360023067473-How-to-Copy-Gateway-ODBC-settings-to-another-server-or-new-data-source) . Then in your C# code, pass the connection string as an argument when calling the OdbcConnection object's constructor, for example:
    
    ```
                <code>
            <span><span><span>var</span></span></span> connectionString = <span><span><span>"DRIVER={ZappySys API Driver};ServiceUrl=https://yourservices.provider.com/api/xxxx....;AuthName=Http;"</span></span></span>;
    
            <span><span><span>using</span></span></span> (<span><span><span>var</span></span></span> conn = <span><span><span>new</span></span></span> OdbcConnection(connectionString))
            {
            <span><span><span>// ...</span></span></span>
            }
        </code>
    ```
    
    **How to get ZappySys Driver Connection String?**
    
    Please follow the instructions below to retrieve the connection string for the ZappySys driver.
    
    1.  Click on the Windows Start menu.
        
    2.  In the search bar, type **ODBC** and press Enter.
        
    3.  From the search results, choose **ODBC Data Sources** or **ODBC Data Sources (32-bit)** or a similar option depending on your system architecture and ODBC driver configuration.
        
    4.  Choose your data source from the list, then click on the **Configure** button.
    5.  After opening the Data Source UI, you should copy the connection string to a Notepad or text file for reference.
    6.  Click on **Copy Connection String** button.  
        When you click 'Copy Connection String,' you may encounter the following option:  
        Choose the third option **All Settings** to copy everything and click on **OK** button.  
        ![zappysys-data-source-copy-connectionstring](https://zappysys.com/api/images/zsdg/zappysys-odbc-driver-copy-settings.png "Copy ZappySys ODBC Driver Connection Settings")  
        ![zappysys-data-source-copy-connectionstring](https://zappysys.com/api/images/zsdg/zappysys-odbc-driver-copy-settings-1.png "Copy ZappySys ODBC Driver Connection Settings")
    
    That's it connection string has been successfully copied.
    
    **How to Overcome the Long Connection String Issue**
    
    This issue is typically caused when the connection string includes a long RefreshToken attribute (i.e. RefreshToken=xxxxxxxxxxxx...xxx, especially if it's more than 1,000 characters).
    
    A good solution is to supply the RefreshToken by a file. Simply copy and paste the RefreshToken into a text file and save it, and then pass that file path in the connection string instead of directly supplying the RefreshToken.
    
    Here is an example of a connection string that can cause the issue:
    
    ```
    
        <span><span><span>var</span></span></span> connectionString = <span><span><span>"Driver={ZappySys API Driver};RefreshToken=xxxxxxxxxxxx...xxxxxxx;ServiceUrl=...;"</span></span></span>;
    
        <span><span><span>using</span></span></span> (<span><span><span>var</span></span></span> conn = <span><span><span>new</span></span></span> OdbcConnection(connectionString))
        {
        <span><span><span>// ...</span></span></span>
        }
    ```
    
    Here is an example of a connection string that has resolved the issue by moving the RefreshToken attribute to the file **c:\\my\_refresh\_token.txt**:
    
    ```
    
        <span><span><span>var</span></span></span> connectionString = <span><span><span>"Driver={ZappySys API Driver};RefreshTokenFile=c:\my_refresh_token.txt;ServiceUrl=...;"</span></span></span>;
    
        <span><span><span>using</span></span></span> (connectionString)
        {
        <span><span><span>// ...</span></span></span>
        }
    ```
    

## Insider Insights

### While using ExecuteNonQuery make sure to use output=0.

Sometime Executing **\`cmd.ExecuteNonQuery\`** in C# didn't trigger the API call immediately specifically for **\`INSERT\`**, **\`UPDATE\`**, or **\`DELETE\`** statement, as it only initiates the call when the iterator is requested. When using ExecuteNonQuery(), it's primarily intended for SQL statements that don't return data, such as UPDATE, INSERT, or DELETE. If you're not seeing any changes made by the UPDATE statement, there could be several reasons for this.

One potential reason, as you've mentioned, is related to deferred execution. In some cases, the changes made by the UPDATE statement might not be visible immediately, **especially if you're not requesting any output from the query. In such cases, explicitly setting Output = 0 can force the iterator to be called, ensuring that the changes are applied.**

**Here's an example of how you might modify your code to include this:**

```

<span><span><span>using</span></span></span> System;
<span><span><span>using</span></span></span> System.Data.Odbc;

<span><span><span>namespace</span></span></span> <span><span><span>ConsoleApp</span></span></span> {
    <span><span><span>class</span></span></span> <span><span><span>Program</span></span></span> {
        <span><span><span><span><span><span>static</span></span></span></span></span><span><span> </span></span><span><span><span><span><span>void</span></span></span></span></span><span><span> </span></span><span><span><span><span><span>Main</span></span></span></span></span><span><span>(</span></span><span></span><span><span></span><span><span></span>) </span></span></span>{
            <span><span><span>var</span></span></span> dsn = <span><span><span>"JiraDSN"</span></span></span>;
            <span><span><span>using</span></span></span> (<span><span><span>var</span></span></span> conn = <span><span><span>new</span></span></span> OdbcConnection(String.Format(<span><span><span>"DSN={0}"</span></span></span>, dsn)))
            {
                conn.Open();
                
                <span><span><span>//We're currently referring to the example with the Products table. Please substitute it with the table of your choice.</span></span></span>
                <span><span><span>var</span></span></span> cmd =<span><span><span>new</span></span></span> OdbcCommand(<span><span><span>"UPDATE Products SET ProductName='Chai' Where ProductID=1 WITH(Output=0)"</span></span></span>, conn);
                
                <span><span><span>//Increase the timeout duration from the default 30 seconds, which may be insufficient in certain scenarios</span></span></span>
                cmd.CommandTimeout=<span><span><span>600</span></span></span>; <span><span><span>// 600-Seconds</span></span></span>
                
                <span><span><span>// Execute the query</span></span></span>
                <span><span><span>int</span></span></span> rowsAffected = cmd.ExecuteNonQuery();

                <span><span><span>// Check the number of rows affected</span></span></span>
                <span><span><span>if</span></span></span> (rowsAffected &gt; <span><span><span>0</span></span></span>)
                {
                    Console.WriteLine(<span><span><span>"Update successful."</span></span></span>);
                }
                <span><span><span>else</span></span></span>
                {
                    Console.WriteLine(<span><span><span>"No rows were updated."</span></span></span>);
                } 
            }
            Console.ReadKey();
        }
    }
}
```

## Create Custom Store Procedure in ZappySys Driver

You can create procedures to encapsulate custom logic and then only pass handful parameters rather than long SQL to execute your API call.

Steps to create Custom Store Procedure in ZappySys Driver. You can insert Placeholders anywhere inside Procedure Body. [Read more about placeholders here](https://zappysys.com/onlinehelp/odbc-powerpack/scr/odbc-format-static-placeholders.htm)

1.  Go to Custom Objects Tab and Click on Add button and Select Add Procedure:  
    ![ZappySys Driver - Add Store Procedure](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-add-custom-store-procedure.png "ZappySys Driver - Add Store Procedure")
    
2.  Enter the desired Procedure name and click on OK:  
    ![ZappySys Driver - Add Store Procedure Name](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-custom-store-procedure-enter-name.png "ZappySys Driver - Add Store Procedure Name")
    
3.  Select the created Store Procedure and write the your desired store procedure and Save it and it will create the custom store procedure in the ZappySys Driver:  
    Here is an example stored procedure for ZappySys Driver. You can insert Placeholders anywhere inside Procedure Body. [Read more about placeholders here](https://zappysys.com/onlinehelp/odbc-powerpack/scr/odbc-format-static-placeholders.htm)  
    
    ```
    <span><span><span>CREATE</span></span></span> <span><span><span>PROCEDURE</span></span></span> [usp_get_orders]
        @fromdate = <span><span><span>'&lt;&lt;yyyy-MM-dd,FUN_TODAY&gt;&gt;'</span></span></span>
     <span><span><span>AS</span></span></span>
        <span><span><span>SELECT</span></span></span> * <span><span><span>FROM</span></span></span> Orders <span><span><span>where</span></span></span> OrderDate &gt;= <span><span><span>'&lt;@fromdate&gt;'</span></span></span>;
    ```
    
      
    ![ZappySys Driver - Create Custom Store Procedure](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-create-custom-store-procedure.png "ZappySys Driver - Create Custom Store Procedure")
4.  That's it now go to Preview Tab and Execute your Store Procedure using Exec Command. In this example it will extract the orders from the date 1996-01-01:  
    
    ```
    <span>Exec</span> usp_get_orders <span>'1996-01-01';</span>
    ```
    
      
    ![ZappySys Driver - Execute Custom Store Procedure](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-execute-store-procedure.png "ZappySys Driver - Execute Custom Store Procedure")
5.  Let's generate the SQL Server Query Code to make the API call using store procedure. Go to Code Generator Tab, select language as SQL Server and click on Generate button the generate the code.  
    As we already created the linked server for this Data Source, in that you just need to copy the Select Query and need to use the linked server name which we have apply on the place of \[MY\_API\_SERVICE\] placeholder.  
    
    ```
    <span><span><span>SELECT</span></span></span> * <span><span><span>FROM</span></span></span> OPENQUERY([MY_API_SERVICE], <span><span><span>'EXEC usp_get_orders @fromdate=''1996-07-30'''</span></span></span>)
    ```
    
      
    ![ZappySys Driver - Generate SQL Server Query](https://zappysys.com/api/images/zs-custom-objects/odbc-driver-generate-sql-server-query-to-call-stored-procs.png "ZappySys Driver - Generate SQL Server Query")
6.  Now go to SQL served and execute that query and it will make the API call using store procedure and provide you the response.  
    ![ZappySys Driver - Generate SQL Server Query](https://zappysys.com/api/images/zs-custom-objects/call-odbc-driver-stored-procs-in-sql-server.png "ZappySys Driver - Generate SQL Server Query")
    

## Create Custom Virtual Table in ZappySys Driver

ZappySys API Drivers support flexible Query language so you can override Default Properties you configured on Data Source such as URL, Body. This way you don't have to create multiple Data Sources if you like to read data from multiple EndPoints. However not every application support supplying custom SQL to driver so you can only select Table from list returned from driver.

If you're dealing with Microsoft Access and need to import data from an SQL query, it's important to note that Access doesn't allow direct import of SQL queries. Instead, you can create custom objects (Virtual Tables) to handle the import process.

Many applications like MS Access, Informatica Designer wont give you option to specify custom SQL when you import Objects. In such case Virtual Table is very useful. You can create many Virtual Tables on the same Data Source (e.g. If you have 50 URLs with slight variations you can create virtual tables with just URL as Parameter setting.

1.  Go to Custom Objects Tab and Click on Add button and Select Add Table:  
    ![ZappySys Driver - Add Table](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-add-custom-table.png "ZappySys Driver - Add Table")
    
2.  Enter the desired Table name and click on OK:  
    ![ZappySys Driver - Add Table Name](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-custom-table-enter-name.png "ZappySys Driver - Add Table Name")
    
3.  And it will open the New Query Window Click on Cancel to close that window and go to Custom Objects Tab.
    
4.  Select the created table, Select Text Type AS SQL and write the your desired SQL Query and Save it and it will create the custom table in the ZappySys Driver:  
    Here is an example SQL query for ZappySys Driver. You can insert Placeholders also. [Read more about placeholders here](https://zappysys.com/onlinehelp/odbc-powerpack/scr/odbc-format-static-placeholders.htm)  
    
    ```
    <span><span><span>SELECT</span></span></span>
      <span><span><span>"ShipCountry"</span></span></span>,
      <span><span><span>"OrderID"</span></span></span>,
      <span><span><span>"CustomerID"</span></span></span>,
      <span><span><span>"EmployeeID"</span></span></span>,
      <span><span><span>"OrderDate"</span></span></span>,
      <span><span><span>"RequiredDate"</span></span></span>,
      <span><span><span>"ShippedDate"</span></span></span>,
      <span><span><span>"ShipVia"</span></span></span>,
      <span><span><span>"Freight"</span></span></span>,
      <span><span><span>"ShipName"</span></span></span>,
      <span><span><span>"ShipAddress"</span></span></span>,
      <span><span><span>"ShipCity"</span></span></span>,
      <span><span><span>"ShipRegion"</span></span></span>,
      <span><span><span>"ShipPostalCode"</span></span></span>
    <span><span><span>FROM</span></span></span> <span><span><span>"Orders"</span></span></span>
    <span><span><span>Where</span></span></span> <span><span><span>"ShipCountry"</span></span></span>=<span><span><span>'USA'</span></span></span>
    ```
    
      
    ![ZappySys Driver - Create Custom Table](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-create-custom-view.png "ZappySys Driver - Create Custom Table")
5.  That's it now go to Preview Tab and Execute your custom virtual table query. In this example it will extract the orders for the USA Shipping Country only:  
    
    ```
    <span><span><span>SELECT</span></span></span> * <span><span><span>FROM</span></span></span> <span><span><span>"vt__usa_orders_only"</span></span></span>
    ```
    
      
    ![ZappySys Driver - Execute Custom Virtual Table Query](https://zappysys.com/api/images/zs-custom-objects/zappysys-driver-custom-virtual-table-preview.png "ZappySys Driver - Execute Custom Virtual Table Query")
6.  Let's generate the SQL Server Query Code to make the API call using store procedure. Go to Code Generator Tab, select language as SQL Server and click on Generate button the generate the code.  
    As we already created the linked server for this Data Source, in that you just need to copy the Select Query and need to use the linked server name which we have apply on the place of \[MY\_API\_SERVICE\] placeholder.  
    
    ```
    <span><span><span>SELECT</span></span></span> * <span><span><span>FROM</span></span></span> OPENQUERY([MY_API_SERVICE], <span><span><span>'EXEC [usp_get_orders] ''1996-01-01'''</span></span></span>)
    ```
    
      
    ![ZappySys Driver - Generate SQL Server Query](https://zappysys.com/api/images/zs-custom-objects/odbc-driver-generate-sql-server-query-to-call-virtual-table.png "ZappySys Driver - Generate SQL Server Query")
7.  Now go to SQL served and execute that query and it will make the API call using store procedure and provide you the response.  
    ![ZappySys Driver - Generate SQL Server Query](https://zappysys.com/api/images/zs-custom-objects/call-odbc-driver-virtual-table-in-sql-server.png "ZappySys Driver - Generate SQL Server Query")
    

## Conclusion

In this article we discussed how to connect to Jira in C# and integrate data without any coding. [Click here to Download](https://zappysys.com/products/odbc-powerpack/download/) **Jira Connector** for **C#** and try yourself see how easy it is. If you still have any question(s) then [ask here](https://zappysys.com/support) or simply click on live chat icon below and ask our expert (see bottom-right corner of this page).

## Actions supported by Jira Connector

Jira Connector support following actions for REST API integration. If some actions are not listed below then you can easily edit Connector file and enhance out of the box functionality.

 Read Get custom field contexts Details

 Read Get custom field contexts Details

## Jira Connector Examples for C# Connection

This page offers a collection of SQL examples designed for seamless integration with the ZappySys [API ODBC Driver](https://zappysys.com/products/odbc-powerpack/odbc-api-driver/) under ODBC Data Source (36/64) or ZappySys Data Gateway, enhancing your ability to connect and interact with Prebuilt Connectors effectively.

#### List fields    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/list-fields)\]

Lists all fields that are used and available in issue entity

#### List projects    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/list-projects)\]

Lists all available projects

#### INSERT Project    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/insert-project)\]

Inserts a single project

```
<span><span><span>INSERT</span></span></span> <span><span><span>INTO</span></span></span> Projects(ProjectKey, <span><span><span>Name</span></span></span>, ProjectTypeKey, LeadAccountId, AssigneeType)
<span><span><span>VALUES</span></span></span> (<span><span><span>'TEST'</span></span></span>, <span><span><span>'Test Project'</span></span></span>, <span><span><span>'software'</span></span></span>, <span><span><span>'70122:XXXXXXXX-XXXX-XXXX-XXXX-c5da8c98b9e2'</span></span></span>, <span><span><span>'PROJECT_LEAD)
WITH (Output=1)'</span></span></span>)
```

#### UPDATE Project    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/update-project)\]

Updates a single project

```
<span><span><span>UPDATE</span></span></span> Projects
<span><span><span>SET</span></span></span> <span><span><span>Name</span></span></span> = <span><span><span>'My Test Kanban Project'</span></span></span>
   ,ProjectCategoryId = <span><span><span>1</span></span></span>
<span><span><span>WITH</span></span></span> (ProjectIdOrKey = <span><span><span>'MYPRJCT'</span></span></span>, <span><span><span>Output</span></span></span>=<span><span><span>1</span></span></span>)
```

#### DELETE Project    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/delete-project)\]

Deletes a single project

```
<span><span><span>DELETE</span></span></span> <span><span><span>FROM</span></span></span> Projects
<span><span><span>WITH</span></span></span> (ProjectIdOrKey = <span><span><span>'10020'</span></span></span>, <span><span><span>Output</span></span></span>=<span><span><span>1</span></span></span>)
```

#### List users    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/list-users)\]

Lists all available users

#### INSERT User    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/insert-user)\]

Inserts a single user

```
<span><span><span>INSERT</span></span></span> <span><span><span>INTO</span></span></span> <span><span><span>Users</span></span></span>(EmailAddress, DisplayName, <span><span><span>Name</span></span></span>, <span><span><span>Password</span></span></span>)
<span><span><span>VALUES</span></span></span> (<span><span><span>'my@user.com'</span></span></span>, <span><span><span>'John Doe'</span></span></span>, <span><span><span>'John'</span></span></span>, <span><span><span>'xhedkspstdadaothoua'</span></span></span>)
<span><span><span>WITH</span></span></span> (<span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

#### DELETE User    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/delete-user)\]

Deletes a single user

```
<span><span><span>DELETE</span></span></span> <span><span><span>FROM</span></span></span> <span><span><span>Users</span></span></span>
<span><span><span>WITH</span></span></span> (<span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>, accountId = <span><span><span>''</span></span></span><span><span><span>547059</span></span></span>:<span><span><span>136095</span></span></span>a0-XXXX-XXXX-XXXX<span><span><span>-3e4</span></span></span>c66f26551<span><span><span>''</span></span></span>)
```

#### List issues    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/list-issues)\]

Lists all available issues across all projects

#### INSERT Issue    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/insert-issue)\]

Inserts a single issue to a particular project

```
<span><span><span>INSERT</span></span></span> <span><span><span>INTO</span></span></span> Issues(ProjectKey, IssueTypeName, Summary, Description)
<span><span><span>VALUES</span></span></span>(<span><span><span>'SMP'</span></span></span>, <span><span><span>'Task'</span></span></span>, <span><span><span>'My ticket inserted through the API'</span></span></span>, <span><span><span>'A description about an issue'</span></span></span>)
<span><span><span>WITH</span></span></span> (<span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

#### UPDATE Issue    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/update-issue)\]

Updates an issue

```
<span><span><span>UPDATE</span></span></span> Issues
<span><span><span>SET</span></span></span> Summary = <span><span><span>'This is my summary'</span></span></span>
   ,Description = <span><span><span>'Lot''s of stuff to describe'</span></span></span>
   ,Labels = <span><span><span>'[ "bugfix" ]'</span></span></span>
   ,DueDate = <span><span><span>'2029-10-10'</span></span></span>
<span><span><span>WITH</span></span></span> (IssueIdOrKey=<span><span><span>'ISSKEY'</span></span></span>, <span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)<span><span><span>'</span></span></span>
```

#### DELETE Issue    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/delete-issue)\]

Deletes a single issue

```
<span><span><span>DELETE</span></span></span> <span><span><span>FROM</span></span></span> Issues
<span><span><span>WITH</span></span></span> (IssueIdOrKey=<span><span><span>'10020'</span></span></span>, <span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

#### List worklogs    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/list-worklogs)\]

Lists all worklogs from all issues

#### INSERT Worklog    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/insert-worklog)\]

Inserts a single worklog to a particular issue

```
<span><span><span>INSERT</span></span></span> <span><span><span>INTO</span></span></span> Worklogs(TimeSpentInSeconds, <span><span><span>Comment</span></span></span>, StartedAt)
      <span><span><span>VALUES</span></span></span>(<span><span><span>7200</span></span></span>,<span><span><span>'My Comment!'</span></span></span>,<span><span><span>'2020-02-23T16:20:30.123+0000'</span></span></span>)
      <span><span><span>WITH</span></span></span> (IssueIdOrKey=<span><span><span>'ISSKEY-1'</span></span></span>, <span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

#### UPDATE Worklog    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/update-worklog)\]

Updates a worklog

```
<span><span><span>UPDATE</span></span></span> Worklogs
<span><span><span>SET</span></span></span> TimeSpentInSeconds = <span><span><span>28800</span></span></span>
   ,<span><span><span>Comment</span></span></span>=<span><span><span>'My Comment!'</span></span></span>
   ,StartedAt=<span><span><span>'2020-01-23T16:20:30.123+0000'</span></span></span>
<span><span><span>WITH</span></span></span> (IssueIdOrKey=<span><span><span>'MTK-1'</span></span></span>, WorklogId=<span><span><span>'123465'</span></span></span>, <span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

#### DELETE Worklog    \[[Read more...](https://zappysys.com/api/integration-hub/jira-connector/help/examples/delete-worklog)\]

Deletes a single worklog of an issue

```
<span><span><span>DELETE</span></span></span> <span><span><span>FROM</span></span></span> Worklogs
<span><span><span>WITH</span></span></span> (IssueIdOrKey=<span><span><span>'10020'</span></span></span>, WorklogId=<span><span><span>'123465'</span></span></span>, <span><span><span>OUTPUT</span></span></span>=<span><span><span>1</span></span></span>)
```

  

## Other App Integration scenarios for Jira

## Other Connectors for C#

  
[Download Jira Connector for C#](https://zappysys.com/products/odbc-powerpack/download/ "Click here to Download Installer for Jira Connector and start C# integration") [Documentation](https://zappysys.com/api/integration-hub/jira-connector/help/odbc-getting-started) 

Common Searches:
