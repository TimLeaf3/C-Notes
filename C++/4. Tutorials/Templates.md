
- Templates are used to declare a type that can be any other type in C++
- For example :

```
template <typename T> //
void print(T value) {
	cout << value << endl;
}
```

Here, the parameter for the `print` function can be a `int`, a `float` ...

To force certain conditions for template types, we can use `static_assert` :
```
template <typename N> //
struct vector {
	static_assert(std::is_arithmetic<N>::value, 
		"error_message if contdition is not respected);
		
	N x, y;
	vector(N x, N y) : x(x), y(y) {} 
}
```
