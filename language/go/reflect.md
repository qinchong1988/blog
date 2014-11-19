## Golang 编程基础之反射

 - 反射可以大大的提高程序的灵活性
 - 反射使用TypeOf和ValueOf函数从接口中获取目标对象信息
 - 反射会将匿名字段作为独立字段(匿名字段的本质)
 - 想要利用反射来修改对象状态，前提是interface.data是settable，即pointer-interface
 - 通过反射可以动态调用方法

##### 首先来看一个反射的基本上使用，主要用到了```reflect.TypeOf()```月```reflect.ValueOf()```

```golang

package test

import (
	"fmt"
	"reflect"
)

type User struct {
	Id   int
	Name string
	Age  int
}

func (u User) Hello() {
	fmt.Println("Hello world.")
}

func TestRelect() {
	u := User{1, "ok", 12}
	//注意：这个位置不能传递&u,除非函数里面做了保护
	Info(u)
}

func Info(o interface{}) {
	t := reflect.TypeOf(o)

	fmt.Println("Type:", t.Name())
	
	if k := t.Kind(); k != reflect.Struct {
		fmt.Println("类型不对无法反射")
		return
	}

	v := reflect.ValueOf(o)
	fmt.Println("Fields:")

	for i := 0; i < t.NumField(); i++ {
		f := t.Field(i)
		val := v.Field(i).Interface()
		fmt.Printf("%6s: %v = %v\n", f.Name, f.Type, val)
	}

	for i := 0; i < t.NumMethod(); i++ {
		m := t.Method(i)
		fmt.Printf("%6s: %v\n", m.Name, m.Type)
	}

}

//输出
Type: User
Fields:
    Id: int = 1
  Name: string = ok
   Age: int = 12
 Hello: func(test.User)

```

##### 接下来我们分析一下匿名字段
我们在定义个Manager类型

```golang

type Manager struct {
	User  //匿名字段
	title string
}

func main(){
    m := Manager{User: User{1, "ok", 12}, title: "123"}
	t := reflect.TypeOf(m)
	//主要是通过索引来获取字段的
	fmt.Printf("%#v\n", t.Field(0)) 
	//要想获得User中Id字段的值，需要传递一个Slice，第一个表示
	//User在Manager中的索引，第二个表示Id在User中的索引
	fmt.Printf("%#v\n", t.FieldByIndex([]int{0, 0}))
}

//输出
reflect.StructField{Name:"User", PkgPath:"", Type:(*reflect.rtype)(0x2d3240), Tag:"", Offset:0x0, Index:[]int{0}, Anonymous:true}
//Anonymous:true表名其是一个匿名字段，要想取得User里面的Id

reflect.StructField{Name:"Id", PkgPath:"", Type:(*reflect.rtype)(0x246ac0), Tag:"", Offset:0x0, Index:[]int{0}, Anonymous:false}
```

如果想要修改某一个变量的值可以按下面的操作

```golang

func main(){
    x := 123
	v := reflect.ValueOf(&x) //注意是取地址
	v.Elem().SetInt(999)
	fmt.Println(x)
	
	u := User{1, "ok", 12}
	set(&u)
	fmt.Println(u)
}	
func set(o interface{}) {
	v := reflect.ValueOf(o)
	if v.Kind() != reflect.Ptr || !v.Elem().CanSet() {
		fmt.Println("传递的类型不对")
		return
	}
	v = v.Elem()

	f := v.FieldByName("Name")
	if !f.IsValid() {
		fmt.Println("Field not found!!!")
		return
	}

	if f.Kind() == reflect.String {
		f.SetString("BYEBYE")
	}

}

```

下面演示下方法的调用

```golang

func (u User) Hello2(name string) {
	fmt.Println("Hello", name, ", my name is ", u.Name)
}

func main(){
    u := User{1, "ok", 12}
    //演示反射调用方法
	v := reflect.ValueOf(u)
	//还不能使用Hello，上面已经定义过的，不支持重载的吗？
	mv := v.MethodByName("Hello2")
	//方法参数传递一个Slice
	args := []reflect.Value{reflect.ValueOf("Joe")}
	mv.Call(args)
}

```