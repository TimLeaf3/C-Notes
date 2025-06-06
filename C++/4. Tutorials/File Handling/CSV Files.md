
- headers :
```
#include <fstream>
#include <iostream>
#include <sstream>
#include <string>
```

#### 1. *Write to File*

- Specify the path to the file

```
std::ofstream file("students.csv"); // Create or overwrite the file

if (!file.is_open()) {
    std::cerr << "Failed to open file.\n";
    return 1;
}
```

- Write to file using the `<<` operator :

```
file << "Name,Age \n";			// Write CSV header

file << "Alice, 20 \n";			// Write some data
file << "Bob, 22 \n";
file << "Charlie, 19 \n";

file.close();
```


#### 2. *Read from File*

- Specify the path to the file

```
std::ifstream file("students.csv");

    if (!file.is_open()) {
        std::cerr << "Failed to open file.\n";
        return 1;
    }

```

- Read from file using `std::getline()` :

```
std::string line;

std::getline(file, line);

while (std::getline(file, line)) {
    std::stringstream ss(line);
    std::string name;
    std::string age;
	
    std::getline(ss, name, ',');
    std::getline(ss, age, ',');
	
    std::cout << "Name: " << name << ", Age: " << age << '\n';
}

file.close();

```


#### *Notes & Tips*

- Always use `std::ios::binary` when opening binary files
- Use `reinterpret_cast<char*>` to treat your data as raw bytes