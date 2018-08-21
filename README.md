# SOLID-Principles-of-Object-Oriented-Design
    S- Single Responsibility Principle
    O- Open/Close Principle
    L- Liskov Substitution Principle
    I- Interface Segregation Principle
    D- Dependency Inversion
    
# 1. Single Responsibility Principle
   "A class or module should have a single responsibility, where a responsibility is nothing but a reason to change."
   
   When we design our classes, we should take care that one class at the most is responsible for doing one task or functionality among the whole set of responsibilities that it has. And only when there is a change needed in that specific task or functionality should this class be changed. 
   
   Also note that the classes defined using the Single Responsibility Principle are inherently cohesive in nature, i.e. their structure – attributes & behavior – are specific to that single functionality only to which the class caters to.
    
  # Use Case: 
   Consider a class that opens a connection to the database, pulls out some table data, and writes the data to a file. This class has multiple reasons to change: adoption of a new database, modified file output format, deciding to use an ORM, etc.  In terms of the SRP, we'd say that this class is doing too much.
  
    Above class may have the following issues:  
    a) More Coupling -  Class is handling more responsibility
    b) More Fragile - class has more than one reason to be changed 
    c) Difficult to code change - Refactoring may leads to break the other functionalities.
  
  Reason why we should use SRP 
    
    a) Low Coupling
    b) Less fragile 
    c) Code Changes
    d) Maintainability

Example:
    
   Below class has multiple responsibilities 
    
    public class Task {

      public Connection openDatabaseConnection(String databaseName) {
        Connection conn = null;
        // Open database connection here
        return conn;
      }

      public String getDataFromTable(Connection conn, String tableName) {
        String userData = "";
        // Get user data from table
        return userData;
      }

      public void writeDataToFile(String data) {
        // Write data to file
      }
    }
    
  Now, we can re-write this call and can break it into following classes to support SRP
  
    public class Task {
      
      private DatabaseHelper mDbHelper;
      private FileSystemHelper mFileSystemHelper;
      
      public Connection performOperation() {
        Connection conn = mDbHelper.openDatabaseConnection("user_database");
        String userData = mDbHelper.getDataFromTable(conn, "user_table");
        mFileSystemHelper.writeDataToFile(userData);
      }
      
    }
  
    public class DatabaseHelper {

      public Connection openDatabaseConnection(String databaseName) {
        Connection conn = null;
        // Open database connection here
        return conn;
      }
      
      public String getDataFromTable(Connection conn, String tableName) {
		    String userData = "";
		    // Get user data from table
		    return userData;
	    }
      
    }
    
    public class FileSystemHelper {
      public void writeDataToFile(String data) {
		    // Write data to file
	    } 
    }
    
   Here we have created DatabaseHelper and FileSystemHelper classes and divided the responsibilities.

# 2. Open/Close Principle
# 3. Liskov Substitution Principle
# 4. Interface Segregation Principle
# 5. Dependency Inversion
