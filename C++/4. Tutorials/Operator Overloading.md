
- To overload an operator, the syntax is like so :
`return_type operator<symbol>(parameter) const;`

- Example with binary + :
```
vector<int> operator+(const vector<int> &other) const {
	return vector<int>(x + other.x , y + other.y);
}
```

- It is possible to overload these types of operators :
	- Arithmetic operators : `+`, `-`, `*`, `/`, `%` 
	- Assignment operator : `=`, `+=`, `-=`, `*=`, ...
	- Comparison operator : `==`, `!=`, `<`, `>`, ...
	- Unary operator : `++`, `--`, `-`, `!`, ...
	- Subscript operator : `[]` 
	- I / O operators : `<<`, `>>` 


- To operate the **insertion** `<<` operator : 
```
std::ostream& operator<< (std::ostream& os, const vector<int> &v) {
	return os << "(" << v.x << ", " << v.y << ")";
}
```



### Notes & Tips

- Use `const` as often as possible to avoid unwanted modifications
- Return by **value** for arithmetic operators, and by **reference** for assignment ones
- 