
#### 1. *Write to File*

- Specify the path to the file

```
std::ofstream outFile("path/to/file.bin, std::ios::binary);

if (!outFile) {
	std::cerr << "Failed to open file" << '\n';
	return 1;
}
```

- Write to file using `reinterpret_cast<char*>`

```
Person person = {"Alice", 30};

outFile.write(reinterpret_cast<char*>(&person), sizeof(person));

outFile.close();
```

`reinterpret_cast<char*>` treats the data as a raw sequence of bytes


#### 2. *Read from File*

- Specify the path to the file

```
std::ifstream inFile("path/to/file.bin", std::ios::binary);

if (!inFile) {
	std::cerr << "Failed to open file" << '\n';
	return 1;
}
```

- Read from file using `reinterpret_cast<char*>`

```
Person person;

inFile.read(reinterpret_cast<char*>(&person), sizeof(person));

inFile.close();
```


#### *Notes & Tips*

- Always use `std::ios::binary` when opening binary files
- Use `reinterpret_cast<char*>` to treat your data as raw bytes