# Introduction

SCDO is an open source blockchain project with its core hosted on [github.com/scdoproject/go-scdo](https://github.com/scdoproject/go-scdo). Compiling go-scdo will produce two main terminal executables, `node` and `client`, which are also available in [github releases](https://github.com/scdoproject/go-scdo/releases). This tutoral will walk through the compiling instructions of go-scdo. The following tutorials in SCDO's wiki "GO-SCDO" section will introduce the usage of these executables while going through different aspects of the SCDO architecture.

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
./node -v
./client -h
```

# Appendix

### Mac 

Developer command line tools would cover git and gcc tools. Install golang with `brew install go`.

### Windows

For golang, use the [msi installer](https://golang.org/dl/) for convenience. After the msi installation, search variables and add the environment variable: name: go, value: C:\Go. For x86_64 architectures, install mingw-w64 and add `C:\Program Files\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0\mingw64\bin` or whatever mingw-w64's bin path is to window's PATH variable. Git also provides an installer, and the environment variable is added similarly.
