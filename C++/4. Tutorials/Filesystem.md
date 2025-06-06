
- Using the `<filesystem>` header
- Using `namespace fs = std::filesystem` 


#### 1. *Check if a file/folder exists* 

```
if (fs::exists("path/to/file.any")) {
	cout << "The file exists" << endl;
}

fs::path p = "somethin";

if (fs::is_regular_file(p)) { 
	cout << "It's a file";
} else if (fs::is_directory(p)) {
	cout << "It's a folder";
} else {
	cout << "Something else (link, shortcut...)";
}
```

- Returns a boolean indicating if a path leads to a folder/file
- Indicates the type of a node


#### 2. *Create/delete nodes* 

```
fs::create_directory("path/to/folder");
```

- Lets you create a folder and/or its subfolders if they don't exist yet


```
fs::remove("my_file.any);
fs::remove_all("my_folder");
```

- Deletes a file
- Recursively deletes a folder and its content


#### 3. *List a folder's content* 

```
for (const auto& entry : fs::directory_iterator("path/to/folder")) {
	cout << entry.path() << '\n';
}

for (const auto& entry : fs::recursive_directory_iterator("folder")) {
	cout << entry.path() << '\n';
}
```

- Iterates over every node in a folder
- Iterates over every node in a folder and its subfolders


#### 4. *Copy a node* 

```
fs::copy("source.any", "folder/copy.any");
fs::copy("source_folder", "target_folder", fs::copy_options::recursive);
```

- Copies a file to a new location with a new name
- Copies a folder and its content to a new location


#### 5. *Move/rename a file* 

```
fs::rename("former_name.any", "new_folder/new_name.any");
```

- Renames a file / moves it if a new folder is given before the new name


#### 6. *Obtain a file's properties* 

```
fs::path p = "path/to/file.any";

cout << "Name: " << p.filename() << '\n';
cout << "Extension: " << p.extension() << '\n';
cout << "Absolute path: " << fs::absolute(p) << '\n';
cout << "Size: " << fs::file_size(p) << " bytes\n";
```

- Get the properties of a file :
	- Its name 
	- Its extension (.txt, .bin, .ini, ...)
	- Its absolute path ("User/username/Documents/...)
	- Its size in bytes (not bits)


#### 7. *Exceptions*

```
std::error_code err;

fs::remove("non-existant_file.txt", ec);
if (err) { 
	cerr << "error : " << err.message() << '\n'; 
}
```


#### *Notes and tips* 


- Never use `std::string` to create a path, instead use `fs::path` 
- Always check if a file exists before manipulating it
- Use `std::error_code` to avoid using `try/catch` 


- To concatenate paths, we use the ' / ' operator, like so : 
```
fs::path base = "folder";
fs::path file = "test.txt";
fs::path full_path = base / file;		// → "folder/test.txt"
```


- To get / set the current working directory, use : 
```
fs::current_path();						// Returns the current path
fs::current_path("new_path");			// Sets  a new current path
```


