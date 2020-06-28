# Introduction

SCDO is an open source blockchain project with its core hosted on [github.com/scdoproject/go-scdo](https://github.com/scdoproject/go-scdo). Compiling go-scdo will produce two main terminal executables, `node` and `client`, which are also available in [github releases](https://github.com/scdoproject/go-scdo/releases). 

- [get](#compiling)
    - Compile `node` and `client`.
    - Environment setup.
- [shard](shard.md)
    - SCDO sharding protocol.
    - Generate keys with `client`.
- [run](run.md): 
    - How to run a miner with `node`.
    - Making a keyfile/keystore with `client`.
- [api](api.md): 
    - How to send transactions with `client`.
    - JSON-RPC references.


# Compiling

Required tools:
```
git --version
gcc --version
go version
```
Environment
```
# terminal
mkdir -p ~/go/src/github.com/scdoproject/
cd ~/go/src/github.com/scdoproject/
git clone https://github.com/scdoproject/go-scdo.git

# command prompt
mkdir %HOMEPATH%\go\src\github.com\scdoproject
cd %HOMEPATH%\go\src\github.com\scdoproject
git clone https://github.com/scdoproject/go-scdo.git
```
Build Command
```
# terminal
cd ~/go/src/github.com/scdoproject/go-scdo
make all

# command prompt
cd %HOMEPATH%\go\src\github.com\scdoproject
buildall.bat
```

Binaries can be found in go-scdo's "build" directory.

```
cd go-scdo/build

# node version
./node -v

# node and client help command
./node -h
./client -h
```

# Appendix

### Mac 

Developer command line tools would cover git and gcc tools. Install golang with `brew install go`.

### Windows

For golang, use the [msi installer](https://golang.org/dl/) for convenience. After the msi installation, search variables and add the environment variable: name: go, value: C:\Go. For x86_64 architectures, install mingw-w64 and add `C:\Program Files\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0\mingw64\bin` or whatever mingw-w64's bin path is to window's PATH variable. Git also provides an installer, and the environment variable is added similarly.
