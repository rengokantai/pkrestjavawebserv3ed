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
