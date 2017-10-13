# How to find a directory on linux?


```
find / -type d -name 'httpdocs'
```
The first parameter "/" is where to look, in this case "/" it's the entire system.

-name could be -iname to ignore case

also -type is not mandatory
