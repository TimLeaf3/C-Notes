
### Structs 

- To create `struct` the syntax is not like in C++, we use the `typedef` keyword, like so :
```
typedef struct {
	char name[50];
	int age;
	float average;
} Student;
```


### Classes 

- To create a `class` in Obj-C, we use the keywords `@interface` / `@implementation`
- Example :

File *Student.h*
```
#import <Foundation/Foundation.h>

@interface Student : NSObject

@property NSString *name;
@property int age;
@property float average;

- (void)display;
- (BOOL)hasPassed;

@end
```

- Everything between `@interface` and `@end` is part of the `Student` class
- Lines starting with `@property` declare class **attributes**
- Lines starting with `- (...)` declare class **methods**


File *Student.m*
```
#import "Student.h"

@implementation Student

- (void)display {
	NSLog(@"Name: %@\nAge: %d\nAverage: %.2f", 
		self.name, self.age, self.average);
}

- (BOOL)hasPassed {
	return self.average >= 10.0;
}

@end
```


File *main.m*
```
#import "Student.h"

int main(void) {
	@autoreleasepool {
		Student *s = [[Student alloc] init];
		s.name = @"Tim";
		s.age = 19;
		s.average = 11.5;
		
		[s display];
		
		if ([s hasPassed])  {
			NSLog(@"%@ has passed ✅", s.name);
		} else {
			NSLog(@"%@ has failed ❌", s.name);
		}
	}
	return 0;
}
```


### Syntaxe

- To declare a class, we use : `@interface` / `@implementation`.
- Attributes are declared with `@property`
- Methods are declared like so `- (return_type)method_name;
- To call methods, the syntax is : `[object methode]`


