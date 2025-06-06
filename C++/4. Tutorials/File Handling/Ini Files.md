
- Using the `SimpleIni.h` header


---
#### Write to File

```
CSimpleIniA ini;
ini.SetUnicode();              // optional : enable UTF-8 support

ini.SetValue("Graphics", "width", "1920");
ini.SetValue("Graphics", "height", "1080");
ini.SetValue("Graphics", "fullscreen", "true");

ini.SetValue("Audio", "volume", "80");
ini.SetValue("Audio", "mute", "false");

SI_Error rc = ini.LoadFile("config.ini");
if (rc < 0)
	return 1;

cout << "INI file written successfully" << endl;
return 1;
```


Output :
```
[Graphics]
width=1920
height=1080
fullscreen=true

[Audio]
volume=80
mute=false
```


---
##### Read from File

```
CSimpleIniA ini;
ini.SetUnicode();              // optional : enable UTF-8 support

SI_Error rc = ini.LoadFile("config.ini");
if (rc < 0)
	return 1;

// Read values with default fallback if key is missing
const char* width = ini.GetValue("Graphics", "width", "800");
const char* height = ini.GetValue("Graphics", "height", "600");
const char* fullscreen = ini.GetValue("Graphics", "fullscreen", "false");

const char* volume = ini.GetValue("Audio", "volume", "100");
const char* mute = ini.GetValue("Audio", "mute", "false");

std::cout << "Graphics Settings:\n";
std::cout << "  Width: " << width << "\n";
std::cout << "  Height: " << height << "\n";
std::cout << "  Fullscreen: " << fullscreen << "\n";

std::cout << "Audio Settings:\n";
std::cout << "  Volume: " << volume << "\n";
std::cout << "  Mute: " << mute << "\n";

return 0;
```


--- 
#### Tips & Notes

- Calling `SetValue(...)` multiple times on the same key `overwrites` it automatically.