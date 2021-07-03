# Golang内存对齐


## 1. Golang如何计算结构体占用空间

在go语言中，使用**unsafe.Sizeof**来获取结构体所占空间字节数。

```go
package main

import (
	"fmt"
	"unsafe"
)
type Good struct {
	a int8
	b int16
	c int32
}

type NotGood struct {
	a int8
	b int32
	c int16
}

func main(){
	fmt.Println(unsafe.Sizeof(Good{}))
	fmt.Println(unsafe.Sizeof(NotGood{}))
}
```

运行上面的例子将会输出 **8，12**

仅仅是因为结构体内字段顺序的不同，这两个结构体占用的空间差了4个字节。这就是内存对齐的结果！

## 2.为什么要内存对齐


