
- En objective-C les fichiers utilisés ont l'extension `.m`.
- Types de base : `NSString`, `NSNumber`, `NSArray`, `NSDictionary`...


### Hello, World!

- To display informations in Objective-C, we use `NSLog()` 
- To print "Hello, World!" :
```
int main(void) {
	@autoreleasepool {
		NSLog(@"Hello, World!");
	}
	return 0;
}
```


### Variables

- Variables follow this structure in Objective-C :
`type name = value;`


- Print a variable's value :
```
int score = 42;
NSLog(@"Score : %d", score);
```

or 

```
int a = 5;
int b = 3;
int somme = a + b;
NSLog(@"%d + %d = %d", a, b, somme);
```


- Most common types in Objective-C :
	- `int`				:	`%d`
	- `unsigned int`		:	`%u`
	- `long`				:	`%ld`
	- `unsigned long`		:	`%lu`
	- `float`				:	`%f`
	- `double`				:	`%g`
	- `char`				:	`%c`
	- `char *`				:	`%s`
	- `NSString *`			:	`%@`
	- `pointeur`			:	`%p`
	- `size_t`				:	`%tu`


- The `const` keyword forbids the variable from changing its value after its declaration


### Functions

- Obj-C functions follow this structure : `return_type name(parameters) {...}`
- Example :
```
int addition(int a, int b) {
	return a + b;
}
```


### Conditions 

- Conditions work in Obj-C just like in C++ 
```
if (a) {
	...
} else {
	...
}
```


### Loops

- Loops also work in Obj-C just like in C++
```
for (int i = 1; i <= 10; i++) {
	NSLog(@"i = %d", i);
}
```

or

```

int i = 0;
while (i < 5) {
	i++;
}
```


### Switch 

- Switches are like `if` / `else` but they take a parameter :
```
switch (a) {
	case 1:
		NSLog(@"a = 1");
	case 2:
		NSLog(@"a = 2");
	default:
		NSLog(@"a is unknown");
}
```


### Arrays

- Tables work like C++ arrays :
```
int notes[5] = {14, 12, 15, 9, 17};
for (int i = 0; i < 5; i++) {
	NSLog(@"Note n°%d : %d", i + 1, notes[i]);
}
```


### NSString

- In Obj-C, `NSString` is nothing like C++ `std::string` :
	- First, `NSString` have to be preceded with a `@`
	- A `NSString` must be declared like so : `NSString* variable_name`

```
NSString *name = @"Tim";
NSString *greeting = [NSString stringWithFormat:@"Hi, %@ !", name];

NSLog(@"%@", greeting) 	 	 	 // displays Hi, Tim!
```


### NSArray

- `NSArray` are a particular type of array :
	- They store ONLY `NSObjects` 
	- They have a dynamic size
	- They are used to work with 

```
NSArray *grades = @[@10, @12];
NSLog(@"First grade : %@", notes[0]);
```

- The numbers in `grades` have a `@` before them because they're not normal `int`, in fact they are `NSNumbers` objects


### NSDictionary

- `NSDictionary` is like a `std::map` in C++, they store `keys` and `values` , and let you access the values via the keys :

```
NSDictionary *notes = @{
	@"Alice" : @14,
	@"Bob" : @17,
	@"Charlie" : @12
};

for (NSString *name **in** notes) {
	NSLog(@"%@ got %@", name, notes[name]);
}
```

- NSDictionary allow you to use a `forin` statement instead of a normal `for` loop


### Tips & Notes

- `@autoreleasepool` manages the memory automatically, it needs to be used in the `main.m` with Command Line Tools in Xcode

- ⚠️ Les objets ne sont pas comme les types de base ⚠️
	- Les types comme `int`, `float` sont **copiés** 
	- Les objets comme `NSString`, `NSArray` sont **référencés** (pointeur)

- Functions with no parameters must have the `void` in place of the parameters in the function declaration, like so :
	- `int getX(void);`		✅
	- `int getX();`			❌

- //