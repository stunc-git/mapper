# devfeel/mapper
A simple mapper tools for different struct or map to struct

## 1. Install

```
go get -u github.com/devfeel/mapper
```

## 2. Getting Started
```go
package main

import (
	"fmt"
	"github.com/devfeel/mapper"
)

type (
	User struct {
		Name string
		Age  int
		Id   string `mapper:"_id"`
		AA   string `json:"Score"`
	}

	Student struct {
		Name  string
		Age   int
		Id    string `mapper:"_id"`
		Score string
	}

	Teacher struct {
		Name  string
		Age   int
		Id    string `mapper:"_id"`
		Level string
	}
)

func init(){
	mapper.Register(&User{})
	mapper.Register(&Student{})
}

func main() {
	user := &User{}
	teacher:= &Teacher{}
	student := &Student{Name: "test", Age: 10, Id: "testId", Score:"100"}

	mapper.Mapper(student, user)
	mapper.AutoMapper(student, teacher)

	fmt.Println("student:", student)
	fmt.Println("user:", user)
	fmt.Println("teacher", teacher)
}

```
执行main，输出：
```
student: &{test 10 testId 100}
user: &{test 10 testId 100}
teacher &{test 10 testId }
```

## Features
* 支持不同结构体相同名称相同类型字段自动赋值
* 支持Mapper与AutoMapper,分别对应是否需要提前Register struct
* 支持map到struct的自动映射赋值，使用MapperMap
* 支持tag标签，tag关键字为 mapper
* 兼容json-tag标签
* 当tag为"-"时，将忽略tag定义，使用struct field name