
### General Syntax :
```
[capture](parameters) -> return_type {
    // function body
};
```

- `[capture]` : captures external variables by value (`=`), reference (`&`) or by their specific name.
- `(params)` : parameters like a normal function (int x, float y....)
- `-> type` : (optional) return type if not obvious
- `{...}` : the function body

#### Capture by value :
```
int x = 5;
[=]() { cout << x << '\n'; }();
```

- captures x by its value


#### Capture by reference :
```
int x = 5;
[&]() { x += 10; }();
```

- captures x by its place in memory


#### With parameters and return type :
```
auto sum = [](int a, int b) -> int {
	return a + b;
};
cout << sum(3, 4);		// prints 7
```
