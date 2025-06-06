
To use the functional library in C++ :


- Include the `<functional>` header


- The blueprint for a `std::function` variable is : 
	`std::function<return_type(arg1_type, arg2_type...)> function_name;`


- You can declare a function and define it using a lambda function :
```
std::function<void()> callback;

callback = []() {
	cout << "Callback" << endl;
}

callback();
```


- You can also pass a function in another function as a parameter :
```
void print(int x) {
	cout << x << endl;
}

void example(int x, std::function <void(int)> &func) {
	func(x);
}

example(3, print); 					// prints '3'
```

