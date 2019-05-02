# C# - Summary

## Class-Design

### Fields
Fields store values within the class.
Allowed access-modifiers: 
```csharp
private ...		// Only accessable from within the class
protected ...	// Only accessable from own class and classes that inherit this class

// Following are also possible, but not recommended
public ...		// Accessable from everywhere
internal ...	// Only accessable from within the namespace
```
Basic field definition:
```csharp
// Definition without assignments
private int myIntField;
private MyObject obj;
private string[] myStringArray;

// Definition with assignments
private float myFloatField = 0.45;
private double[] myDoubleArray = new double[5];
private long[] myLongArray = new long[] { 1, 4, 7 };
```

Advanced field definition:
```csharp
// Static fields
private static String companyName;
```
___
### Properties
Properties can get and set fields with additional checks, conditions or operations.
```csharp
private int squareWidth;
private int xPosition;
private int yPosition;

// Property with set-condition
public int SquareWidth
{
	get { return squareWidth; }
	set
	{ 
		if(value >= 0) squareWidth= value;
		else squareWidth= 0;
	}
}

// Readonly-Property
public int Area
{
	get { return squareWidth * squareWidth; }
}

// Default Get/Set Property
public int XPosition
{
	get { return xPosition; }
	set { xPosition = value; }
}

// Alternative Style
public int YPosition
{
	get => yPosition;
	set => yPosition = value;
}

// Auto-Implemented Properties (no field required)
public int ZPosition { get; set; }
```
___
### Methods
```csharp
// Method without return value or Parameters
public void MyMethod()
{ 
	// ...
}

// Method with return value and one parameter
public int MyReturnMethod(int inParameter)
{
	// ...
	return outparameter;
}

// Method with optional parameters
public void MyOptionalParamMethod(int required, float optional = 1.5)
{
	// ...
}

// Static Method
public static void MyStaticMethod(float maxValue)
{
	// ...
}

// Overloading Methods
public double MyOverloadedMethod(int inputValue) 
{
	// ...
	return outparameter;
}
public double MyOverloadedMethod(float inputValue)
{
	// ...
	return outparameter;
}
```

___
### Indexer
An indexer is mostly like a property for an array:

Standard use for an indexer:
```csharp
private int[] myArray= new int[] { 1, 4, 7, 12 };

public int this[int idx]
{
	set { myArray[idx] = value; }
	get { return myArray[idx]; }
}
```

Use indexer with keywords:
```csharp
string[] days = { "Sun", "Mon", "Tues", "Wed", "Thurs", "Fri", "Sat" }; 

private int GetDay(string testDay) 
{ 
	for (int j = 0; j < days.Length; j++) 
	{ 
		if (days[j] == testDay) { return j; } 
	} 
}

public int this[string day] 
{ 
	get { return (GetDay(day)); } 
}
```
___
### Constructor
```csharp
class MyClass
{
	private int myField1;
	private int myField2;

	// Default Constructor
	public MyClass()
	{
	}
	
	// Overloading constructors
	public MyClass(int _myField1, int _myField2)
	{
		myField1 = _myField1;
		myField2 = _myField2;
	}
	
	// Extending constructors
	public MyClass(int _myField1):this(_myField1,0) { }
}
```
___
### Overriding Methods
Methods can be overridden and the behaviour of the Method can be changed.
```csharp
public override string ToString()
{
	// ...
}
```
___
### Operation Overloading
Operators for classes can be overridden and givven new functionality.
```csharp
public static int operator+ (int a, int b)
{
	// ...
	return c;
}
```
___
### Enumerations
```csharp
public enum MyEnum 
{
	VAL1,
	VAL2,
	VAL3
};
```
___
## Arrays & Lists
### Definition of Arrays
```csharp
// Creating array without assigning
private int[] myArray;

// Creating array with fixes lenght
private int[] myArray;
myArray = new int[3];
// OR
private int[] myArray = new int[3];

// Creating pre-filled array
private string[] myArray = new string[] { "Str1" , "Str2" , "Str3" };

// Alternative syntax
private string[] myArray = { "Str1" , "Str2" , "Str3" };

// Creating a 2-Dimentional array
private int[,] myMultiDimensionalArray = new int[2,3];

// Creating a jagged array
private int[][] myJaggedArray = new int[6][];
myJaggedArray[0] = new int[4];

// Filling an array made from objects
private MyObject[] objArray = new MyObject[5];

for(int i = 0 ; i < objArray.lenght ; i++)
{
	objArray[i] = new MyObject();
}
```
___
### Definition of Lists
```csharp
// Defining List
private List<int> myList = new List<int>();

myList.add(50);
```
___
## Generic Datatypes
### Creating Generic class
```csharp
public class MyGenericClass<T>
{
	private T[] elements;
	private int count;
	
	public MyGenericClass(int size)
	{
		elements = new T[size];
	}
}
```
___
## Interfaces
### Creating an Interface
```csharp
public interface IMyInterface
{
	void MethodThatMustBeImplemented(string param);
}
```
___
### Assigning an Interface
```csharp
// Assigning to a default class
public class MyClass : IMyInterface, IMyOtherInterface
{
	// ...
}

// Assigning to a generic class
public class MyClass<T> where T : IComparable
{
	// ...
}
```
___
### IComparable Interface
```csharp
class MyClass : IComparable
{
	public int CompareTo(object obj)
	{
		if( ... ) return -1; // objX is bigger than this object
		if( ... ) return 1; // objX is smaller than this object
		return 0;	// both objects are the same
	}
}
```
___
### IDisposable Interface
```csharp
class MyClass : IDisposable
{
	private bool isDisposed = false;

	~MyClass
	{
		// Deconstructor actions
		Dispose();
	}
	
	public void Dispose()
	{
		if(!isDisposed)
		{
			isDisposed = true;
			// e.g. objectCounter--;
			GC.SuppressFinalize(this);
		}
	} 
}
```
___
## Exception Handling
### Basic Exception Functions
```csharp
// Throwing Exception
throw new Exception("Error-Message");

// Force exception-test
checked { a *= b }

// try-catch-finally
try
{
	// Try Executing code
}
catch (IndexOutOfRangeException ioorEx)
{
	// Catch an Index-Out-Of-Range exception
}
catch(Exception ex)
{
	// Catch other exceptions
}
finally
{
	// Execute functions that must be done after try as well as catch.
	// E.g. Saving file, Closing SQL-Connection, ...
}
```
___
### Exception Types
The following list shows some exception-types of the .NET Framework.
```csharp
Exception
SystemException
IndexOutOfRangeException
NullReferenceException
AccessViolationException
InvalidOperationException
ArgumentException
ArgumentNullException
ArgumentOutOfRangeException
ExternalException
COMException
SEHException
```
___
## Inheritance
### Access-Keywords
By using the `protected`-Keyword, the fields can be accessed by the cild-classes.
```csharp
protected int xPosition;
```
___
### Inheriting a class
Inherit everything from the parent-class:
```csharp
class MyChildClass : MyParentClass
{
	// ... 
}
```
___
### Abstract
Abstract Class: Can not be created as an object. Used as parent-class
for child-classes. E.g.: Shape-Class -> child: Rectangle.
```csharp
abstract class MyBaseClass
{
	// ...
}
```
Abstract Method: Must be implemented in every child-class.
```csharp
public abstract int MyAbstractMethod();
```
___
### Virtual
Declared in Parent-Class. Allows for the method to be overridden.
```csharp
public virtual int MyVirtualMethod()
{
	// ...
}
```
___
### Sealed
The `sealed` keyword prevents the method from beeing overridden.
```csharp
public sealed int MySealedMethod()
{
	// ...
}
```
___
### Override
Overrides the methods declaration in the parent-class.
```csharp
public override int MyVirtualMethod()
{
	// ...
}
```
To keep all functions from the parent-method and add more functions, use the `base` keyword:
```csharp
public override int MyVirtualMethod()
{
	base.MyVirtualMethod();
	// ...
}
```
___
### Constructors
To Inherit the functionality of the parent-constructor, use the `base`-Keyword:
```csharp
public MyChildClass(int _x, int _y, int _r): base(_x, _y)
{
	// ...
}
```
___
## Unit-Tests
### Unit-Test Basics
#### Naming Test-Methods:
- The Method that should be tested
- The scenario that should be tested
- The expected result
#### Parts of a Test-Method
- Arrange
-- Create the start-conditions
- Act
-- Execute the test
- Assert
-- Check the result
___
### Defining a Test-Class & Test Methods
```csharp
[TestClass]
public class UnitTest
{
	// ...
}

[TestMethod]
public void MyTestMethod()
{
	// ...
}
```
___
### Calling Test-Method with DataRows
```csharp
[DataTestMethod]
[DataRow( "funcParam1" , "funcParam2" )]
[DataRow( "FUNCPARAM1" , "FUNCPARAM2" )]
[DataRow( "funcparam1" , "funcparam2" )]
public void MyTestMethod(string param1, string param2)
{
	// ...
}
```
___
### Calling Test-Method with expected exception
```csharp
[TestMethod]
[ExpectedException(typeof(ApplicationException))]
public void MyTestMethod()
{
	// ...
}
```
___
### Asserting Results
```csharp
Assert.IsTrue(myBooleanValue);
Assert.AreEqual(myObject1, myObject2);
Assert.IsNotNull(myObject);
```
Checking float-values
```csharp
const double delta = 1e-04;	// 4 floating points
```
```csharp
Assert.AreEqual(myFloatValue1, myFloatValue2, delta);
```
___
## SQL - ODBC
### Connection-Strings
```csharp
// Connection-String MS-Access
string conStr = @"Driver={Microsoft Access Driver (*.mdb, *.accdb)};Dbq=" + Application.StartupPath + @"\MyDatabase.accdb;Uid=Admin;Pwd=;";
```

```csharp
// Connection-String MySQL
string conStr = @"Driver={MySQL ODBC 3.51 Driver};Server=IP-or-Adresse;Database=dbname;User=dbuser;Password=dbpass;Option=3;";
```
___
### Basic SQL-Class
The following class is a simple ODBC-Class for basic SQL-Functions
```csharp
class SQLC
{
	private static OdbcConnection connection = null;
	
	// Open and close connections within the program with
	// SQLC.Connection.Open(); or SQLC.Connection.Close();
	public static OdbcConnection Connection
	{
		get
		{
			if(connection == null)
			{
				string conStr = @"Driver={...}";
				connection = new OdbcConnection(conStr);
			}
			return connection;
		}
	}

	// Get the result-set of an SQL-Query
	public static OdbcDataReader ExecuteQuery(string sql, params object[] vals)
	{
		OdbcCommand cmd = new OdbcCommand(sql,Connection);
		foreach(object parameter in vals) cmd.Parameters.AddWithValue("",parameter);
		OdbcDataReader reader = cmd.ExecuteReader();
		return reader;
	}
	
	// Execute a Non-Query
	public static int ExecuteNonQuery(string sql, params object[] vals)
	{
		OdbcCommand cmd = new OdbcCommand(sql,Connection);
		foreach(object parameter in vals) cmd.Parameters.AddWithValue("",parameter);
		Connection.Open();
		int result = cmd.ExecuteNonQuery();
		Connection.Close();
		return result;
	}
	
	// Execute a Scalar
	public static object ExecuteScalar(string sql, params object[] vals)
	{
		object o;
		OdbcCommand cmd = new OdbcCommand(sql,Connection);
		foreach(object parameter in vals) cmd.Parameters.AddWithValue("",parameter);
		Connection.Open();
		o = cmd.ExecuteScalar();
		Connection.Close();
		return o;
	}
}
```
___
### Usage of SQLC-Class
Using the `ExecuteQuery()` Method:
```csharp
SQLC.Connection.Open();
OdbcDataReader reader = SQLC.ExecuteQuery("SELECT ...");
while(reader.Read()) lbxList.Items.Add(reader["tableColumn"]);
SQLC.Connection.Close();
```

Using the `ExecuteNonQuery()` Method:
```csharp
SQLC.ExecuteNonQuery("UPDATE ...");
```

Using the `ExecuteScalar()` Method:
```csharp
object o = SQLC.ExecuteScalar("SELECT ...");
if(o != null) txb.Text = o.ToString();
```
___
### Data-Handling with SQLC-Class
Creating a DataTable:
```csharp
public static DataTable CreateDT(string sql)
{
	OdbcDataAdapter da = new OdbcDataAdapter(sql,Connection);
	DataTable dt = new DataTable();
	da.Fill(dt);
	return dt;
}
```
Using the DataTable-Object for Listboxes:
```csharp
DataTable dt = SQLC.CreateDT("SELECT ...");
lbx.DisplayMemeber = "Column1";
lbx.ValueMember = "Column2";
lbx.DataSource = dt;
```
Using the DataTable-Object for DataGridViews:
```csharp
DataTable dt = SQLC.CreateDT("SELECT ...");
dgv.DataSource = dt;
```
___
### SQL-Transactions
```csharp
OdbcTransaction trans = null;
try
{
	SQLC.Connection.Open();
	trans = SQLC.Connection.BeginTransaction();
	cmd.Transaction = trans;
	// Execute SQL-Statements here
	trans.Commit();
}
catch(Exception ex) trans.Rollback();
finally SQLC.Connection.Close();

```
___
## Classes
### String
```csharp
string myStr = "This is a test String";

// Analyse and manipulate Strings
myStr.StartsWith("This");	// -> true
myStr.Split(" ");			// -> ["This","is","a","test","String"]
myStr.SubString(6); 		// -> "s a test String"
myStr.SubString(6,7);		// -> "s a tes"
myStr.Replace(' ','-');		// -> "This-is-a-test-String"

// Haystack-Needle
if(hayStack.IndexOf(needle) != -1)
{
	// Found!
}
else 
{
	// Not Found!
}
```
___
### StringBuilder
```csharp
StringBuilder sb = new StringBuilder();

sb.Append("Text 1 ");
sb.AppendFormat("Text {0}", 1);

string finalString = sb.ToString();
```
___
### StreamReader
```csharp
StreamReader sr = new StreamReader("filePath.txt");
while(sr.Peek() >= 0)
{
	outString = sr.readLine();
}
sr.Close();
```

```csharp
StreamReader sr = new StreamReader("filePath.txt");
while((outString = sr.ReadLine()) != null)
{
	// ...
}
sr.Close();
```
___
### StreamWriter
```csharp
StreamWriter sw = new StreamWriter ("filePath.txt");

string myName = "Tom"
sw.writeLine("I am {0}", myName);

sw.Close();
```
___
### Math
```csharp
// Usefull Math-Class Methods
Math.PI;			// -> 3.141...
Math.Abs(-5);		// -> 5
Math.Sqrt(16);		// -> 4
Math.Pow(8,2);		// -> 64
Math.Sin(82);		// -> sin(82)
Math.Cos(39);		// -> cos(39)
Math.Round(4.8);	// -> 5
```
___
### Random
```csharp
Random rnd = new Random();
int randomInt = rnd.Next(0,100);
```
___
## Forms & Dialogs
### Message-Boxes
Show a message-box
```csharp
MessageBox.Show("Message","Title",MessageBoxButton.OK);
```
Get output from message-box
```csharp
if(MessageBox.Show("Content","Title",MessageBoxButtons.OKCancel) == DialogResult.OK)
{
	// ...
}
```
___
### Read Key-Inputs
```csharp
e.KeyChar == 13;
```
___
### Close a Form
```csharp
this.Close();
```
___
### Open File Dialog
```csharp
// Open File with Dialog
ofdOpen.InitialDirectory = Enviroment.GetFolderPath(Enviroment.SpecialFolder.Desktop);

if(ofdOpen.ShowDialog() == DialogResult.OK)
{
	StreamReader sr = new StreamReader(ofdOpen.Filename);
	while((outString = sr.ReadLine()) != null)
	{
		// ...
	}
	sr.Close();
	MessageBox("Loading Successfull");
}
```
___

### Data Handling
#### Data Row View
```csharp
// E.g.: Extract Data from Listbox
DataRowView drv = (DataRowView) lbx.SelectedItem;
string value1 = drv["Column1"].ToString();
string value2 = drv["Column2"].ToString();
```
#### DataGrid
```csharp
// Create the DataTable-object
DataTable dtGrid = new DataTable();
// Add Columns to Grid
dtGrid.Columns.Add("ColumnName1",typeof(int));
dtGrid.Columns.Add("ColumnName2",typeof(string));

// Fetch data for grid (e.g. from other grid)
DataTable dtDataRaw = (DataTable)(dgv.DataSource)

// Add rows to grid
DataRow newRow;
newRow = dtGrid.NewRow();
newRow["Column1"] = 5;
newRow["Column2"] = "Content";

// Add row to grid
dtGrid.Rows.Add(newRow);

// Add data to grid
dgv.DataSource = dtGrid;
```
___
## Form Graphics
### Graphics-Setup
```csharp
// Move center to middle of screen
e.Graphics.TranslateTransform(pbx.Width / 2, pbx.Height / 2);

// Set cartesian coordinate system
e.Graphics.ScaleTransform(-1,1);

// Enable Anti-Aliasing
e.Graphics.SmoothingMode = SmoothingMode.AntiAlias;
```
___

### Drawing Arrows
```csharp
Point p1 = new Point(0,0);
Point p2 = new Point(8,6);
Pen pen = new Pen(Color.red,5);
AdjustableArrowCap aac = new AdjustableArrowCap(5,5,true);

pen.CustomEndCap = aac;
pbx.Invalidate();
e.Graphics.DrawLines(pen, p1, p2);

```
___
## Date handling / Date functions
### Creating DateTime-Objects
```csharp
// Create a default DateTime-Object with the value `01-01-0001 00:00:00`
DateTime dt = new DateTime();

// Create DateTime-Object with current time
DateTime dt = DateTime.Now;

// Create DateTime-Object with set date
DateTime dt = new DateTime(1999, 11, 16);

// Create DateTime-Object with set date and time
DateTime dt = new DateTime(1999, 11, 16, 18, 42, 0);
```
### Output DateTime-Objects
```csharp
// Pre-Defined methods
Console.WriteLine(DateTime.Now.ToShortDateString());
Console.WriteLine(DateTime.Now.ToLongDateString());
```
```csharp
// Region-Specific output
var culture = new System.Globalization.CultureInfo("en-US");  
Console.WriteLine(DateTime.Now.ToString(culture.DateTimeFormat));
```
```csharp
// Custom formats
DateTime dt = new DateTime(2042, 12, 24, 18, 42, 0);  
  
Console.WriteLine(dt.ToString("MM'/'dd yyyy"));		// > 12/24 2042		  
Console.WriteLine(dt.ToString("dd.MM.yyyy"));  		// > 24.12.2042
Console.WriteLine(dt.ToString("MM.dd.yyyy HH:mm"));	// > 12.24.2042 18:42
Console.WriteLine(dt.ToString("dddd, MMMM (yyyy): HH:mm:ss")); // > Wednesday, december (2042)
Console.WriteLine(dt.ToString("dddd @ hh:mm tt",
System.Globalization.CultureInfo.InvariantCulture)); // > Wednesday @ 06:42 PM
```
___
## File handling
### Combine path and filename
```csharp
string fileName = "test.txt"; 
string path = @"C:\Users\Public\TestFolder"; 

string filePath = System.IO.Path.Combine(path, fileName); 
```
___
### Copy a file
```csharp
// Copy 1 file
if (!System.IO.Directory.Exists(targetPath)) 
{ 
	System.IO.Directory.CreateDirectory(targetPath); 
} 

System.IO.File.Copy(sourceFile, destFile, true);
```

```csharp
// Copy a directory
if (System.IO.Directory.Exists(sourcePath) && System.IO.Directory.Exists(targetPath)) 
{ 
	string[] files = System.IO.Directory.GetFiles(sourcePath); 

	foreach (string s in files) 
	{ 
		fileName = System.IO.Path.GetFileName(s); 
		destFile = System.IO.Path.Combine(targetPath, fileName); 
		System.IO.File.Copy(s, destFile, true); 
	} 
} 
```
___
### Rename / Move a file
```csharp
// Move a file
string sourceFile = @"C:\Users\Public\public\test.txt"; 
string destinationFile = @"C:\Users\Public\private\test.txt"; 

System.IO.File.Move(sourceFile, destinationFile); 
```

```csharp
// Move a directory
string sourceDir = @"C:\Users\Public\public\test"; 
string destinationDir = @"C:\Users\Public\private"; 

System.IO.Directory.Move(sourceDir, destinationDir); 
```
___
### Delete a file
```csharp
// Delete a file
if(System.IO.File.Exists(@"C:\Users\Public\DeleteTest\test.txt")) 
{ 
	try 
	{ 
		System.IO.File.Delete(@"C:\Users\Public\DeleteTest\test.txt"); 
	} 
	catch (System.IO.IOException e) 
	{ 
		Console.WriteLine(e.Message); 
	} 
}
```

```csharp
// Delete directory and all subdirectories
if(System.IO.Directory.Exists(@"C:\Users\Public\DeleteTest")) 
{ 
	try 
	{ 
		System.IO.Directory.Delete(@"C:\Users\Public\DeleteTest", true); 
	} 
	catch (System.IO.IOException e) 
	{ 
		Console.WriteLine(e.Message); 
	} 
}
```
___
## Usefull functions
### C# Properties
```csharp
// Setting Property
Properties.Settings.Default.MyProperty = "My Value";

// Get Property
string str = Properties.Settings.Default.MyProperty;
```
___
### String formating types
```csharp
"\r\n"
// OR
Enviroment.NewLine
```
___
### Remove duplicates from Array
```csharp
for(int i = 0; i < myArray.lenght; i++)
{
	for(int j = i + 1; j < myArray.lenght; j++)
	{
		if(myArray[i]==myArray[j]) 
		{
			myArray.RemoveAt(j);
			j--;
		}
	}
}
```
___
### Culture Info
```csharp
var culture = new System.Globalization.CultureInfo("de-AT");
```

Usefull Culture Coutry-Codes
|Country|Code|
|--|--|
|German (Germany)|de-DE|
|German (Austria)|de-AT|
|German (Switzerland)|de-CH|
|English (UK)|en-GB|
|English (USA)|en-US|
|English (Australia)|en-AU|
___
### Debuging
```csharp
Debug.print("Test-Output");
```
___
