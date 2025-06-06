
#### 1. *Write to File*

- Specify the path to the file

```
std::ofstream outFile("output.txt);

if (!outFile) {
	cerr << "Failed to open file" << '\n';
	return 1;
}
```

- Write to file using the `<<` operator

```
outFile << "Hello, file!\n" ;
outFile << "This is line 2.";

outFile.close();
```


#### 2. *Read from File*

- Specify the path to the file

```
std::ifstream inFile("output.txt");

if (!inFile) {
	cerr << "Failed to open file" << '\n';
	return 1;
}
```

- Read from file using a `string` to store the file's content

```
std::string line;

while(std::getline(inFile, line)) {
	cout << "Read: " << line << '\n';
}

inFile.close();
```


#### 3. *Read & Write from File* 

- Use `fstream` with `std::ios::out | std::ios::in | std::ios::app` 

```
std::fstream file("output.txt", ios::in | ios::out | ios::app);

if(!file) {
	cerr << "error opening file" << endl;
	return 1;
}

file << "Appending a new line.\n";

// Move cursor back to the beginning
file.seekg(0);

std::string line;
while(std::getline(file, line)) {
	cout << "Line: " << line << '\n';
}

file.close();
```


#### 4. *Store the content of a file* 

- Use a `std::ostringstream` buffer 

```
ifstream inFile("output.txt");

std::ostringstream buffer;
buffer << inFile.rdbuf();
std::string content = buffer.str();

inFile.close();
```


#### *Notes & Tips*

- Use the headers `<fstream>` `<sstream>` and `<string>`
- Always check if the file is open with  `file.is_open()` 
- Use `std::ios::app` to append to a file instead of overwriting it
