#. 在Docker环境中交叉编译Gopher


如下源代码保存在`$GOPATH`，尝试编译`$GOPATH`下的一个具体应用程序名字叫`BillProcess`

```
docker run --rm -it -v "$GOPATH":/usr/src/myapp -w /usr/src/myapp/src/goBillProcess -e GOOS=windows -e GOARCH=386 -e GOPATH=/usr/src/myapp -e GO15VENDOREXPERIMENT=1 golang:1.6 bash

for GOOS in windows;do for GOARCH in 386 amd64; do go build -v -o BillProcess-$GOOS-$GOARCH-v20160506.exe; done; done
```

如果您仅有一个应用程序在`$GOPATH`下，可以使用如下命令
```
docker run --rm -it -v "$GOPATH":/usr/src/myapp -w /usr/src/myapp/src -e GOOS=windows -e GOARCH=386 -e GOPATH=/usr/src/myapp -e GO15VENDOREXPERIMENT=1 golang:1.6 bash

for GOOS in windows;do for GOARCH in 386 amd64; do go build -v -o main-$GOOS-$GOARCH-vyyyymmdd.exe; done; done
```

在启动容器时，默认设定目标操作系统Windows，系统架构386，可以简单理解成编译出来的程序适用于Windows XP 32位机器。