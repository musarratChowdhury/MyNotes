```
using Newtonsoft.Json; // add reference to Newtonsoft.Json library

string jsonString = File.ReadAllText("path/to/json/file.json");

// deserialize the json string into an object
dynamic jsonObject = JsonConvert.DeserializeObject(jsonString);

// iterate through the json object and build the SQL query
string sqlQuery = "INSERT INTO example_table (";
foreach (var property in jsonObject)
{
sqlQuery += property.Name + ", ";
}

// remove the last comma and space
sqlQuery = sqlQuery.TrimEnd(new char[] { ',', ' ' });

sqlQuery += ") VALUES (";
foreach (var property in jsonObject)
{
sqlQuery += "'" + property.Value + "', ";
}

// remove the last comma and space
sqlQuery = sqlQuery.TrimEnd(new char[] { ',', ' ' });

sqlQuery += ");";

Console.WriteLine(sqlQuery);
```