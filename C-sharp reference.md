```c#
// Creating a hasmap
	var dic = new Dictionary<string,string>(); 
// checking if a key exist
dic.ContainsKey(key);
dic.ContainsValue(value);
//
// iterating each key, value par
foreach (var pair in dic){
pair.Key;
pair.Value;
}
```