# proguard-retrace-guide
---

## Dependency addition

You will exclude the package in **proguard.txt** file found in java/main/resources. 
For example, if the group id is -> com.google.gson, then add this to proguard.txt -> 
-keep, includedescriptorclasses public class com.google.\** { *; }
---

###Download Proguard
1) Download proguard JARs from https://drive.google.com/drive/folders/10SjOR8BzAEsMfoA5A_fCfGYrpqOUYetY?usp=sharing
2) This should contain the following 3 JARs ->
 
        proguard-retrace-5.0.jar
        proguard-gui-5.0.jar
        proguard-base-5.0.jar

## Re-trace obfuscated stacktrace

#### GUI METHOD
***This method is quite self explanatory once you have opened the GUI***
1) To view the GUI, **Run** 
    
        java -jar proguardgui.jar [-nosplash]


####COMMAND LINE METHOD 

1) You will need your ProGuard’s mapping.txt file and the stack trace (Ex: stacktrace.txt) that you want to de-obfuscate.
2) The easiest way to do the next step is copy both these files into a location.
3) **Run** 
    
        java -jar proguard-retrace-5.0.jar -verbose mapping.txt stacktrace.txt > out.txt
        
4) The out.txt will have the appropriate stacktrace.

###Example

 ***Retraced through GUI***
#####Input

    
    java.sql.SQLSyntaxErrorException: Table 'increff.mrp_bucket' doesn't exist
	    at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(Unknown Source)
	    at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(Unknown Source)
	    at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(Unknown Source)
	    at com.mysql.cj.jdbc.ConnectionImpl.execSQL(Unknown Source)
	    at com.mysql.cj.jdbc.StatementImpl.executeUpdateInternal(Unknown Source)
	    at com.mysql.cj.jdbc.StatementImpl.executeLargeUpdate(Unknown Source)
	    at com.mysql.cj.jdbc.StatementImpl.executeUpdate(Unknown Source)
	    at com.mchange.v2.c3p0.impl.NewProxyStatement.executeUpdate(Unknown Source)
	    at com.increff.iris.core.util.DBUtils.executeQuery(Unknown Source)
	    at com.increff.iris.core.module.upload.DatabaseLoaderModule$1.run(Unknown Source)
	    at java.lang.Thread.run(Thread.java:748)



#####Output

    java.sql.SQLSyntaxErrorException: Table 'increff.mrp_bucket' doesn't exist
    	at com.mysql.cj.jdbc.exceptions.SQLError.java.sql.SQLException createSQLException(java.lang.String,java.lang.String,com.mysql.cj.api.exceptions.ExceptionInterceptor)(Unknown Source)
                                              java.sql.SQLException createSQLException(java.lang.String,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,boolean,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,boolean,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
    	at com.mysql.cj.jdbc.exceptions.SQLError.java.sql.SQLException createSQLException(java.lang.String,java.lang.String,com.mysql.cj.api.exceptions.ExceptionInterceptor)(Unknown Source)
                                              java.sql.SQLException createSQLException(java.lang.String,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,boolean,com.mysql.cj.api.exceptions.ExceptionInterceptor)
                                              java.sql.SQLException createSQLException(java.lang.String,java.lang.String,int,boolean,java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)
    	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.java.sql.SQLException translateException(java.lang.Throwable,com.mysql.cj.api.exceptions.ExceptionInterceptor)(Unknown Source)
                                                          java.sql.SQLException translateException(java.lang.Throwable)
    	at com.mysql.cj.jdbc.ConnectionImpl.com.mysql.cj.api.jdbc.result.ResultSetInternalMethods execSQL(com.mysql.cj.jdbc.StatementImpl,java.lang.String,int,com.mysql.cj.api.mysqla.io.PacketPayload,boolean,java.lang.String,com.mysql.cj.api.mysqla.result.ColumnDefinition)(Unknown Source)
                                         com.mysql.cj.api.jdbc.result.ResultSetInternalMethods execSQL(com.mysql.cj.jdbc.StatementImpl,java.lang.String,int,com.mysql.cj.api.mysqla.io.PacketPayload,boolean,java.lang.String,com.mysql.cj.api.mysqla.result.ColumnDefinition,boolean)
    	at com.mysql.cj.jdbc.StatementImpl.long executeUpdateInternal(java.lang.String,boolean,boolean)(Unknown Source)
    	at com.mysql.cj.jdbc.StatementImpl.long executeLargeUpdate(java.lang.String)(Unknown Source)
                                        long executeLargeUpdate(java.lang.String,int)
                                        long executeLargeUpdate(java.lang.String,int[])
                                        long executeLargeUpdate(java.lang.String,java.lang.String[])
    	at com.mysql.cj.jdbc.StatementImpl.int executeUpdate(java.lang.String)(Unknown Source)
                                        int executeUpdate(java.lang.String,int)
                                        int executeUpdate(java.lang.String,int[])
                                        int executeUpdate(java.lang.String,java.lang.String[])
    	at com.mchange.v2.c3p0.impl.NewProxyStatement.int executeUpdate(java.lang.String,int[])(Unknown Source)
                                                   int executeUpdate(java.lang.String,int)
                                                   int executeUpdate(java.lang.String)
                                                   int executeUpdate(java.lang.String,java.lang.String[])
    	at com.increff.iris.core.util.DBUtils.void executeQuery(java.lang.String,java.lang.String)(Unknown Source)
    	at com.increff.iris.core.module.upload.DatabaseLoaderModule$1.void run()(Unknown Source)
    	at java.lang.Thread.run(Thread.java:748)
    	

**@Author** ***Hitesh Sethiya***
