# devfeel/mapper
A simple mapper tools for different struct

## 1. Install

```
go get -u github.com/devfeel/mapper
```

## 2. Getting Started
```go
type (
	User struct {
		Name string
		Age  int
		Id   string
		AA   string `mapper:"Score"`
		CC 	 string
	}

	Student struct {
		Name  string
		Age   int
		Id    string
		Score string
	}
)

func main() {
    mapper.Register(&User{})
	mapper.Register(&Student{})
	user := &User{}
	student := &Student{Name: "test", Age: 10, Id: "testId", Score:"100"}

	mapper.Mapper(student, user)

	fmt.Println(student)
	fmt.Println(user)
}

```

## Features
* 支持不同结构体相同名称相同类型字段自动赋值
* 支持tag标签，tag关键字为 mapper