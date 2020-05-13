---
title:  "Getting Started with WebAssembly"
date: 2020-04-21
published : true
description :   
categories: 
   -  Tutorials 
tags : 
   - notes
   - webdevelopment
   - webassembly
---

## What is it?
* A new revolutionary technology that makes it possible to execute high level language functions in webpages to run at near native speed.
* Browsers interpret Javascript line by line and compile the frequently used code to binary, this is called Just-in-Time (JIT) Compilation.
* To improve this performace, WebAssembly was developed. WebAssembly does not define a programming language.
* However, it allows developers to _code_ webpages using high-level programming languages such as __C/C++__, __Rust__, __Go__
* The _code_ is compiled into a binary module format defined by WebAssembly that can be loaded in to a browser and executed.
* WebAssembly relys on binary instruction and there is no need for JIT compilation, which ensures the code run at near native speed.
* I am in using __C/C++__ for WebAssembly

## What you should know
* Solid __C/C++__
* Basic Javascript and HTML 

## Emscipten
* Provides commandline utility to compile __C/C++__ to WebAssembly binary files

### Installation
#### Pre-requisites
* Common  : Python (>2.7), CMake, Git
* Windows : PyWin32, C/C++ compiler
* Linux   : Node.js
* Mac     : Node.js and Xcode

#### **emsdk** 
* Download from [Github](https://github.com/juj/emsdk)
* Run the emsdk script form top level directory
  ``` shell
  emsdk update
  emsdk install sdk-upstream-master-64bit
  emsdk activate sdk-upstream-master-64bit
  ```
* I got the error 
    >Error: Downloading URL 'https://storage.googleapis.com/webassembly/emscripten-releases-builds/deps/node-v12.9.1-darwin-x64.tar.gz': <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1045)>

    >Warning: Possibly SSL/TLS issue. Update or install Python SSL root certificates (2048-bit or greater) supplied in Python folder or https://pypi.org/project/certifi/ and try again.

    >Installation failed!
  
  Fix was to run the follwing command 
  ```shell
  /Applications/Python\ 2.7/Install\ Certificates.command 
  ```
  if this didnt work, then instead of _emsdk_, run the _emsdk.py_

  ``` shell
  python ./emsdk.py update
  python ./emsdk.py install sdk-upstream-master-64bit
  python ./emsdk.py activate sdk-upstream-master-64bit
  ```
* Update Environment Variables 
  ``` shell 
  source ./emsdk_env.sh 
  ``` 
* Binaries of intrest to us 
  - emcc   - Compiles C code 
  - em++   - Compiles C++ code 
  - emmake - emscripten make utility 
  - emrun  - Launches webserver to run the code

### Compilation and Execution
* _emcc_ compiles C code and the usage is simiilar to _gcc_
  To compile 
   ``` shell
   emcc <flags> <input_files>
   ```
* Flags
  - _-v_ - Verbose
  - _-o filename_ - Output file name
  - _-O level_ - Optimization level
  - _-g_ - include debug info
  - _--emrun_ - output to be aware of emrun
  - _-s option=value_ - Sets Configuration Settings Value

* Configuration Settings 
  - __WASM=1__  --> Generate WebAssembly
  - __ONLY_MY_CODE=1__ --> Doesnt include std library
  - __EXPORTED_FUNCTIONS=__'[<_function_>]' --> Functions to be exported to WebAssembly
  - __SIDE_MODULE=1__ --> Generate Dynamic library (*.wasm)

* Default output without __SIDE_MODULE__ will be a html file ,a javascript file and webAssembly file with __.wasm__ extension
* With the __SIDE_MODULE=1__  compiler will generate only a library file with __.wasm__ extension
* To run the code, use _emrun_ 
  ```shell
  emrun <output.html>
  ```
  command which will start a webserver on
  > Default URL: http://localhost:6931

* We can set the host address and port number using --host and --port flag

* Here is a [Hello world](https://github.com/abilashjram/WebAssembly/tree/master/HelloWorld) example


