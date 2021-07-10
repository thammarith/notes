# Command Line Interface

## Create a new directory and enter it

`$_` is the last argument given to the previous command. In this case, the name of the directory you just created. (Unlike `!$` that refers to the last argument given in the last command in the bash history)

```bash
mkdir directoryName && cd $_
```
