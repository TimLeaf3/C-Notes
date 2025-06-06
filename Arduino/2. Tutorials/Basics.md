----------------------------------------------------------------
The structure of the code in Arduino is like so :
```
void setup() {
	// Runs once when the board is powered or reset
}

void loop() {
	// Runs over and over forever
}
```

- `setup()` is used to initialize things like pin modes, sensors, etc.
-   `loop()` is where the main code runs repeatedly.

The syntax is the same as in C++


----------------------------------------------------------------
Basic types

In Arduino code, variables can have those types :

| type         | size    | range                           |
| :----------- | :-----: | ------------------------------: |
| int          | 2 bytes | -32'768 to 32'767               |
| long         | 4 bytes | -2'147'483'648 to 2'147'483'647 |
| float        | 4 bytes | ±3.4x10⁻³⁸ to ±3.4x10³⁸         |
| double       | 4 bytes | same as float                   |
| char         | 1 byte  | -128 to 127 (ASCII)             |
| boolean      | 1 byte  | `true` or `false`               |
| byte         | 1 byte  | 0 to 255                        |
| unsigned int | 2 bytes | 0 to 65'535                     |

To declare a variable : `type variableName = value;`


----------------------------------------------------------------
Functions

Functions in Arduino code are like in Cpp :
```
returnType functionName(parameters) {
	// body
	return value;
}
```


----------------------------------------------------------------
Common Functions

- `pinMode(pin, mode);` 
	- `pin` :  the pin to behave either as en input or output
	- `mode` :  can be `INPUT`, `OUTPUT`  (or `INPUT_PULLUP`)

- `digitalWrite(pin, value);` 
	- `pin` :  the pin to set the value to 
	- `value` :  can be `HIGH` or `LOW` 

- `digitalRead(pin);` 
	- `pin` : the pin from which we read the value
	- returns either `HIGH` or `LOW` 

- `analogRead(pin);` 
	- `pin` : the pin from which we read the value
	- returns a value from `0` to `1023` (10bits ADC res)

- `analogWrite(pin, value);` 
	- `pin` : the pin to write to 
	- `value` : the value to write from `0` (off) to `255` (on)

- `delay(ms);` 
	- pauses the program for `ms` milliseconds

- `millis();` 
	- returns an `unsigned long int` representing the number of milliseconds since the board began running

- `Serial.begin(baudrate);` 
	- Initializes serial communication at the specified baud rate (bits/s)

- `Serial.print(data);` / `Serial.println(data);`
	- Displays `data` to the serial monitor

- `tone(pin, frequency);` / `tone(pin, frequency, duration);`
	- Generate a square wave of the specified `frequency` on a `pin` (to play sounds)

- `noTone(pin);`
	- Stops the tone

- `constrain(value, min, max);` 
	- Constrains a number to be within a range (`min` → `max`)
