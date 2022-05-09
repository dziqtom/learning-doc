##GIT

###CRLF issue
The problem is standard conversion of line ending in windows and in linux. Standard in allianz is to use linux lf.\
That requires to set up git configuration to make conversion of line end:

```
$ git config --global core.autocrlf input

$ git config --global core.autocrlf true
``` 

