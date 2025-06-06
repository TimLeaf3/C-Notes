
### String formatting

- To format strings, we can use the `<sstream>` lib :
```
#include <string>
#include <sstream>

int x = 23;
std::stringstream ss;

ss << "x = " << x;
```
 
 - `ss` now equals `"x = 23"` 
