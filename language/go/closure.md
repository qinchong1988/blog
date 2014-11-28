##### go语言闭包


```go

package test

import (
	"fmt"
)

func TestColsure() {
	f := closure(10)
	fmt.Println(f(1))
	fmt.Println(f(2))
}

func closure(x int) func(int) int {
	fmt.Printf("%p\n", &x)
	return func(y int) int {
		fmt.Printf("%p\n", &x)
		return x + y
	}
}

// 输出如下
0xc208000898
0xc208000898
11
0xc208000898
12

```
