
#### 1. *Write to File*

- `#include <nlohmann/json.hpp>`
- Create the data struct to be written using `nlohmann::json` data type

```
nlohmann::json j;
j["name"] = "Leaf";
j["age"] = 19;
j["language"] = {"C++", "Python", "Javascript"};
```

- Dump the data into a file using `std::ofstream`

```
std::ofstream out("path/to/file.json");
if (out.is_open()) {
	out << j.dump(4);   // Pretty print with 4-space indentation
	out.close();
} else {
	cerr << "failed to open file" << endl;
	return 1;
}
```


#### 2. *Read from file*

- Get the file containing your json data

```
std::ifstream in("path/to/file.json");
if (!in.is_open()) {
	cerr << "failed to open file" << endl;
	return 1;
}
```

- Get the data from the file 

```
nlohmann::json j;
in >> j;

cout << { j["name"] } << endl;
...
```


#### *Notes & Tips*

- `.dump()` can also be used with no arguments to write compact JSON
- If your file may not exist or can be corrupted, you should add exception handling using :
`try { ... } catch(_) { ... }` 