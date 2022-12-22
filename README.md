# Python requests module binary

# Description

This is the python requests module which includes all its core modules in single file.
I cythonize this file in order to maintain some performance and security.
This is only for arm-v8 (64-bit) android termux.

# Usage

First download this repo, this repo include two files one is cython binary which provide requests module and other is ca certificate bundle file.  
Add both of files in the same folder with your script in which you want to import requests module.  
In your script where you import requests module just change this code.  

```python
# change
import requests #don't import internal requests
# to
from t import requests #import from binary
```
Also don't import this binary directly in python interpreter command line, always use a script to import this module.

# Must follow this instruction

I compile this module in single binary because people can manipulate your python script which use requests module by internally edit requests module files.  
But using this doesn't make you program security fully secure, with this module also impediment your security in your program.  
  
#### Some precautions you should take while using this module

In your script before import requests module must check two things.  
First check there should be no folder with "t" name  
Like this
```python
#you can use my code or better to implement your own check
import posix
import sys
try:
    posix.lstat('t') # encrypt this string
    sys.exit()
except OSError:
    pass
#this code check if there is t name folder in current directory
#if it found then it terminate the program otherwise not
```
Second you should check the hash of binary file
Like this
```python
import _md5
import sys
try:
    f = open('t.cpython-311.so','rb')
    if _md5.md5(f.read()).hexdigest() != '3442961b450c58b8ed316223ec72ce0b': #encrypt file name and hash strings
        sys.exit()
    else:
        f.close()
except:
    sys.exit()
```
##### Last words
There is no security which 100% secure
