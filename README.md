# pkrestjavawebserv3ed
## Java APIs for JSON Processing
### A brief overview of JSON

### Processing JSON data
Two models
- Object model
- Streaming model: data can be read or written in blocks. 

### Processing JSON with JSR 353 object model APIs
```
javax.json.Json
javax.json.JsonReader
javax.json.JsonWriter
```

### Generating the object model from the JSON representation
```
//Import statements for the core classes 
import java.io.InputStream; 
import javax.json.JsonArray; 
import javax.json.JsonReader;   
//Get input stream for reading the specified resource. 
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json"); 
// Create JsonReader to read JSON data from a stream  
Reader reader = new InputStreamReader(inputStream, "UTF-8"); 
JsonReader jsonReader = Json.createReader(reader); 
// Creates an object model in memory. 
JsonArray employeeArray = jsonReader.readArray(); 
```

know the relationship
```
JsonArray
JsonValue
JsonObject
```



### JSON value types
```
try(InputStream inputStream = getClass().getResourceAsStream(jsonFileName);
Reader reader = new InputStreamReader(inputStream, "UTF-8");            
JsonReader jsonReader = Json.createReader(reader))
```
Note:
- Once you have finished using the inputStream, outputStream, JsonReader, or JSonWriter objects, make sure that you close them to release the associated resources. 
- The try-with-resources available from Java 1.7 is used to release resources automatically once the application stops. 
- This is applicable only when the resource implements the __java.lang.AutoCloseable__ interface.



### Generating the JSON representation from the object model
```
import javax.json.Json; 
import javax.json.JsonArray; 
import javax.json.JsonArrayBuilder; 
import javax.json.JsonObject; 
import javax.json.JsonObjectBuilder; 
import javax.json.JsonWriter; 
import java.io.FileOutputStream; 
import java.io.OutputStream;   
// Creates a JsonArrayBuilder instance that is 
// used to build JsonArray 
JsonArrayBuilder jsonArrayBuilder = Json.createArrayBuilder();  
//Get a list of Employee instances. 
// We are not interested in the implementation details of the 
// getEmployeeList() method used in this example. 
List<Employee> employees = getEmployeeList();  
//Iterate over the employee list and create JsonObject for each item 
for (Employee employee : employees) {  
//Add desired name-value pairs to the JSON object and push 
// each object in to the array.   
jsonArrayBuilder.add(Json.createObjectBuilder()
.add("employeeId",employee.getEmployeeId())
.add("firstName", employee.getFirstName())
.add("lastName", employee.getLastName())
.add("email", employee.getEmail())
.add("hireDate", employee.getHireDate()));} 
//Return the json array holding employee details 
JsonArray employeesArray = jsonArrayBuilder.build();  
//write the array to file 
OutputStream outputStream = new FileOutputStream("emp-array.json"); 
JsonWriter jsonWriter = Json.createWriter(outputStream); 
jsonWriter.writeArray(employeesArray);  
//Close the stream to clean up the associated resources 
outputStream.close(); 
jsonWriter.close(); 
```
