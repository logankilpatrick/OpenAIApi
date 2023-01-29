<a name="readme-top"></a>

# OpenAI API Library for C++

This is Community-maintained OpenAI API Library for modern C++, provides access to the OpenAI API to implementing in C++ applications. The some part of the code in this library follow [OpenAPI specification](https://github.com/openai/openai-openapi) and was generated by the [OpenAPI Generator](https://openapi-generator.tech) (check out for other programming languages)..

## Dependencies

Dependencies:
- [CMake](https://cmake.org/download/) (optional if you want to build on Linux or MacOS)
- [Visual Studio Community 2022](https://visualstudio.microsoft.com/downloads/) (for Windnows Only you can build with solution file)
- [vcpkg](https://github.com/microsoft/vcpkg)
- [OpenSSL](https://www.openssl.org/source/) (this is need to build libcurl, because for endpoits using https protocol)
- [Libcurl](https://curl.se/download.html)
- [nlohmann/json](https://github.com/nlohmann/json) JSON libraries, integrated in project don't need to download

## Installations

#Library installation on Linux

You can compile and install the library with these commands:

```sh
$ git clone https://github.com/svgmaster/OpenAIApi
$ cd OpenAIApi/build
$ cmake ..
$ make -j4
$ sudo make install
```

#Library installation on MacOS

You can install dependencies with these commands:

```sh
brew install gcc cmake openssl curl
```

You can compile and install the library, same like Linux instructions.

#Library installation on Windows

Build on Windows with Visual Studio (VS2022)

Prerequisites:
```cmd
vcpkg install curl:x64-windows
```
- Open folder containing source code
- Select 'OpenAIApi.sln' solution file
- Once visual studio opens.
- Select Build > Build Solution.


## Usage

The library needs to be configured with your account's secret key, which is available on the [website](https://beta.openai.com/account/api-keys). We recommend setting it as an environment variable. Here's an example of initializing the library with the API key and Organization Key loaded from an environment variable and creating a completion:

**Important note: Don't expose your secret API key. [See here](https://beta.openai.com/docs/api-reference/authentication) for more details.**

** When build your solution for Windows don't forget to add this library "Ws2_32.lib" "Wldap32.lib" "Crypt32.lib" to linker ** [See here](https://stackoverflow.com/questions/4176503/unresolved-symbols-when-linking-a-program-using-libcurl) for details.

```cpp
#include <iostream>

#include <OpenAIApi/Client.h>
using namespace OpenAIApi;

int main()
{
	std::string apiKey = getenv("OPENAI_API_KEY"); // get API key for authentication
	std::string orgId = getenv("OPENAI_ORG_ID"); // optional specify which organization is used for an API request
	
    Client* client = new Client( apiKey, orgId );
    
    std::string response = client->createCompletion({
        {"model", "text-davinci-002"},
        {"prompt" , "Say this is an example"},
        {"temperature", 0},
        {"max_tokens", 10}
        })
        ["choices"][0]["text"];
		
	delete client; // always free up memory :)	
		
	std::cout << response << std::endl;
	
	return 0;
}        
```

Check out the [full API documentation](https://beta.openai.com/docs/api-reference?lang=curl) for examples of all the available functions.

Or follow this link [Best practices for prompt engineering with OpenAI API](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api).

### Error handling

API requests can potentially return errors due to invalid inputs or other issues. These errors can be handled with a `try...catch` statement:

```cpp
try 
{
    Client* client = new Client( apiKey, orgId );
    
    std::string response = client->createCompletion({
        {"model", "text-davinci-002"},
        {"prompt" , "Say this is an example"},
        {"temperature", 0},
        {"max_tokens", 10}
        })
        ["choices"][0]["text"];
		
	delete client; // always free up memory :)	
		
	std::cout << response << std::endl;
}
catch (std::runtime_error e) 
{
    std::cout << e.what() << std::endl;
}
```

## ChangeLog

[ChangeLog]

## Licence
[The MIT License]

<p align="right">(<a href="#readme-top">back to top</a>)</p>