# Kvpbase Stream Proxy

Stream interface for an object stored on Kvpbase Storage Server (minimum version 3.1).

Kvpbase Storage Server is a RESTful object storage platform written in C# and available under the MIT license.  

Using this stream proxy provides an interface enabling primary storage and data access use cases for objects stored on Kvpbase.

With v1.0.1, KvpbaseStream now supports both .NET Core 2.0 and .NET Framework 4.6.2.

## Help and Feedback

First things first - do you need help or have feedback?  Contact me at joel dot christner at gmail dot com or file an issue here. 

## Getting Started

Be sure to have a Kvpbase Storage Server (https://github.com/kvpbase/storage-server) instance running with your users and containers created and files that you wish to access via stream in the containers.

Refer to the ```KvpbaseStreamTest``` project for a full example.

```
using KvpbaseStreamProxy;

static KvpbaseStream _Stream;

class Program
{
	_Stream = new KvpbaseStream(
		"Your API key",
		"Your user GUID",
		"Your endpoint, i.e. http://localhost:8000/",
		"Your container name",
		"Your object name"
		);

	// seek to the beginning of the stream
	_Stream.Seek(0, System.IO.SeekOrigin.Begin);	// or .Current or .End

	// display the length of the stream
	Console.WriteLine(_Stream.Length);

	// display the position of the stream
	Console.WriteLine(_Stream.Position);

	// write data to the stream
	byte[] data = Encoding.UTF8.GetBytes("Hello, world!");
	_Stream.Write(data, 0, data.Length);

	// seek to the beginning and read 13 bytes
	_Stream.Seek(0, System.IO.SeekOrigin.Begin);
	_Stream.Read(data, 0, 13);
	Console.WriteLine(Encoding.UTF8.GetString(data));  // Hello, world!
}
```
 
## New in v1.0.1

- Retarget to support both .NET Core 2.0 and .NET Framework 4.6.2.

## Version History

Notes from previous versions (starting with v1.0.0) will be moved here.

v1.x
- Initial release
