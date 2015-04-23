#### 最简单的声明panic和恢复recover机制

```go

func TestPanic() {
	A()
	B()
	C()
}

func A() {
	fmt.Println("Func A")
}

func B() {
	defer func() {
		if err := recover(); err != nil {
			fmt.Println("catch panic B")
		}
	}()
	panic("Panic in B")
}

func C() {
	fmt.Println("Func C")
}

```

结果

```
Func A
catch panic B
Func C
```