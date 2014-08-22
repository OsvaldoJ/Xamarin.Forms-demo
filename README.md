Xamarin.Forms-demo
==================

This repository contains C# code to build a Xamarin.Forms app that 
uses Zumero to sync data from the Zumero demo server at 
http://demo.zumero.com:8080.  In addition the code demonstrates some
best practices for handling data conversion, concurrent access, and 
backgrounding for different mobile platforms.

This code was generated by the Zumero App Generator (ZAG). If you 
want to generate a custom version of this app, using your own SQL 
Server tables, visit http://zumero.com/dev-center/zss/#zag.

Shared Code
----

Xamarin.Forms supports housing almost all of the application's code in
a shared Portable Class Library (PCL). The interesting directories are:

 - `demo.Shared/Models`: Contains SQLite-net (https://github.com/praeclarum/sqlite-net)
bindings for each of the tables in the demo dbfile. These bindings enable you to 
use rich .NET objects in code, which are written to the SQLite database in a way 
that Zumero can sync those changes to a remote Zumero server. For information on 
which SQL Server column types need to be handled specially, see 
http://zumero.com/docs/zumero_for_sql_server_manager.html#data_type_conversion_and_limitations.

 - `demo.Shared/Data`: Contains services which can be found via Xamarin.Forms 
the DependencyService.Get<>() method.  

    - The `DataService.cs` file handles loading the database connection, and is coded 
    to handle concurrent database operations (so that a query or update will not fail 
    if a Zumero Sync operation is running).

    - The `SyncService.cs` file handles calling the Zumero Sync operation, and exposing 
    a method to check if a sync is currently running.  The Android application overrides
    this service, in order to insure that the sync is called from a background service.
    
 - `demo.Shared/xaml`: Contains the XAML and C# code-behind definitions for all 
    pages in the application. 

Platforms
----

The amount of platform-specific code is as small as possible.  The platforms 
supported are iOS, Android and Windows Phone 8.


Zumero App Generator
----

The Zumero App Generator creates useful example code by examining the SQL Server tables
that you have exposed through your Zumero server. Generating code for other platforms and
languages is supported as well.  For videos walking through setting up Zumero, or using 
ZAG to generate code, see http://zumero.com/howto/.

Contact
----

If you have questions about this demo, please contact support@zumero.com.
