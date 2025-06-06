
- Using the header only library `<curl.h>`
- Using the API `"https://pokeapi.co"` 

#### 1. *WriteCallback function* 

```
static size_t WriteCallback(void *contents, size_t size, 
							 size_t nMemb, std::string *output) {
	
	size_t totalSize = size * nMemb;
	
	output->append((char*)contents, totalSize);
	
	return totalSize;
}
```

👉 This is a function that `libcurl` calls when it receives data from the server

- _contents_ points to the chunk of data received.

- _size_ is the size of each chunk element (usually 1).

- nMemb is the number of elements received.

- _output_ is a pointer to your string buffer (response) where you want to store the downloaded data.

#### 2. *Setup curl* 

```
CURL *curl = curl_easy_init(); 
// Initialize a CURL handle for making the HTTP(S) request

std::string response; 
// String to hold the API response data

if (curl) { 
// If CURL was successfully initialized
	
	curl_easy_setopt(curl, CURLOPT_URL, 
	 "https://pokeapi.co/api/v2/pokemon/eevee"); 
	 // Set the URL to fetch (Eevee data from PokeAPI)
	
	curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION, WriteCallback); 
	// Set the callback function to handle incoming data
	
	curl_easy_setopt(curl, CURLOPT_WRITEDATA, &response); 
	// Provide the string to store the received data
	
	curl_easy_setopt(curl, CURLOPT_USERAGENT, "libcurl-agent/1.0");
	// Set a user-agent for the HTTP request
	
	CURLcode res = curl_easy_perform(curl); 
	// Perform the HTTP GET request
	
	if (res == CURLE_OK) { 
	// Check if the request was successful
		
		cout << "OK\n" << endl; 
		// Print "OK" if the request succeeded
	} else {
		
		cerr << "Request failed: " << curl_easy_strerror(res) << endl;
		// Print the error message if request failed
	}
	
	curl_easy_cleanup(curl); 
	// Clean up and release CURL resources
	
}
```

#### 3. *Parse data in JSON* 

- using `nlohmann-json` ([[JSON Files]])

```
auto json = nlohmann::json::parse(response); 
// Parse the JSON response into a JSON object

cout << "Name: " << json["name"] << endl; 
// Output the Pokémon's name from the JSON data

cout << "ID: " << json["id"] << endl; 
// Output the Pokémon's ID from the JSON data
```
