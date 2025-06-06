
- Just like in C or C++, you can separate Objective-C in `.m` / `.h` files
- For example :

File *utils.h* 
```
#import <Foundation/Foundation.h>

void greet(NSString *name);
```

File *utils.m* 
```
#import "utils.h"

void greet(NSString *name) {
	NSLog(@"Hello, %@", name);
}
```

- You can then call this function in `main.m` :
```
#import "utils.h"

int main(void) {
	@autoreleasepool {
		greet(@"Tim");
	}
	return 0;
}
```


### Notes & Tips

- Instead of `#include` like in C, we use `#import` in Obj-C