# Fork features

* better support for encoded asp files, mainly recursively decoding all encoded tags until none are left
* better support for scripting: no wait for keypress when finished and actually respect the outputfile name provided on the commandline

Main motivation is so that can be used to decode a full application like this: `grep -irFl '#@~^' | while read i; do ./vbeDecoder.exe -i $i -o ${i/.asp/.dec.asp}; done`


# vbeDecoder
Decoder for Visual Basic Script Encoded scripts (VBE) and JScript Encoded scripts (JSE), written in C#, and provided as a library for .Net Standard.

# What is a VBE ?
The obfuscated VBE and JSE scripts are the result of a proprietary encoding of VBS (Visual Basic Script) and JS (JScript) scripts introduced by Microsoft in version 5 of those. 

The intention was to give script authors the possibility to keep their source code confidential by obfucating it. 
While this feature has been abandoned by most developers, it is now very popular among malware writers to obfuscate their script in a easy way.

Various script formats can be encoded in this way:
- client scripts (`<script language="VBScript.Encode"`)
- the server scripts of the classic ASP pages (`<%@Language="VBScript.Encode"`)
- script files (`.vbs` => `.vbe`)

Developers / malware authors can encode their scripts by using the Microsoft's 'screnc.exe' command-line tool:
```batch
screnc.exe in.htm out.htm
```

# Library 

## Nuggets 

You can use the library by using Nuget package. For this purpose, please use one of the following methods.

***Package Manager***
```
Install-Package vbeDecoder -Version 1.0.0
```

***.NET CLI***
```batch
dotnet add package vbeDecoder --version 1.0.0
```

## How to use ?

It's as simple as it sounds.

***Decoding a file :***
```C#
decodedScript = ScriptDecoder.DecodeFile(encodedScriptPath)
```

***Decoding a raw script from a string:***
```C#
decodedScript = ScriptDecoder.DecodeScript(encodedRawScript)
```

***Decoding a raw script from a stream:***
```C#
decodedScript = ScriptDecoder.DecodeStream(stream)
```

# CLI
## How to use ?

***Arguments:***
```
  --stdin         (Group: input) (Default: false) Read from stdin

  -i, --input     (Group: input) (Default: true) Input files to be processed.

  -o, --output    Output path.

  --help          Display this help screen.

  --version       Display version information.
 ```

 ***Windows:***
 ```
 vbeDecoder.CLI.Core -i script.vbe -o decoded_script.vbs
 ```

 ***Mutli-platform:***
  ```
  dotnet vbeDecoder.CLI.Core.dll  -i script.vbe -o decoded_script.vbs
  ```
