---
icon: code
description: Golang training
---

# Golang

## 1. Development Environment

### Install
```bash
# Download and Install
# https://go.dev/doc/install

# Managing Go installations
# https://go.dev/doc/manage-install

# Installing from source
# https://go.dev/doc/install/source
```

### Goland
```bash
# active
cat ./ideaActive/ja-netfilter-all/ja-netfilter/readme.txt

# plugins
gradianto # themes
rainbow brackets # json
```

## 2. ProjectManage

```bash
go mod init go-example

go mod tidy

go mod vendor
```


## 3. Basic grammar

### Commentary

```go
/*
Go programs doc.

Usage:

    gofmt [flags] [path ...]

The flags are:

    -x xxx
    -y yyy
*/
package main
import "fmt"

func main() {
    fmt.Println("hello world!") // Oneline comment

}
// go doc tmp.go
```

### Constants
```go
type ByteSize float64

const (
    _           = iota // ignore first value by assigning to blank identifier
    KB ByteSize = 1 << (10 * iota)
    MB
    GB
    TB
    PB
    EB
    ZB
    YB
)
func (b ByteSize) String() string {
    switch {
    case b >= YB:
        return fmt.Sprintf("%.2fYB", b/YB)
    case b >= ZB:
        return fmt.Sprintf("%.2fZB", b/ZB)
    case b >= EB:
        return fmt.Sprintf("%.2fEB", b/EB)
    case b >= PB:
        return fmt.Sprintf("%.2fPB", b/PB)
    case b >= TB:
        return fmt.Sprintf("%.2fTB", b/TB)
    case b >= GB:
        return fmt.Sprintf("%.2fGB", b/GB)
    case b >= MB:
        return fmt.Sprintf("%.2fMB", b/MB)
    case b >= KB:
        return fmt.Sprintf("%.2fKB", b/KB)
    }
    return fmt.Sprintf("%.2fB", b)
}
```

### Variables
```go
// option1
var (
    x string
    y int
)
x,y = "a",2
// option2
var x,y = "a",2
// option3
x,y := "a",2

// anonymous variable
_, _ = call_function()
```

### Basic data type
```go

package main
import (
    "fmt"
    "reflect"
)

func main() {
    // bool
    /*
        true
        false
    */
    var b1 = true
    var b2 = false
    fmt.Println(reflect.TypeOf(b1), reflect.TypeOf(b2))

    // float
    /*
        float32
        float64
    */
    var f1 float32 = 3.1234567890123456789
    f1 = 2e10
    fmt.Println(f1, reflect.TypeOf(f1))
    var f2 float64 = 3.1234567890123456789
    f2 = 2e-2
    fmt.Println(f2, reflect.TypeOf(f2))

    // int
    /*
        int8	-128~127
        uint8	0~255
        int16	-32768~32767
        uint16	0~65535
        int32	-2147483648~2147483647
        uint32	0~4294967295
        int64	-9223372036854775808~9223372036854775807
        uint64	0~18446744073709551615
        uint	32-bit operating system is uint32,64-bit operating system is uint64
        int     32-bit operating system is int32,64-bit operating system is int64
    */
    var i int = 10
    fmt.Printf("%d \n", i)  // 10
    fmt.Printf("%b \n", i)  // 1010
    fmt.Printf("%o \n", i)  // 12
    fmt.Printf("%x \n", i)  // a

    // string
    /*
        \r	回车符（返回行首）
        \n	换行符（直接跳到下一行的同列位置）
        \t	制表符
        \'	单引号
        \"	双引号
        \\	反斜杠
    */
    var s string = "hello world"
    s1 := s[1:3]
    s2 := string(s[0]) + string(s[4])
    s3 := `
text line one
text line two
`
    fmt.Println(s1, s2, s3)

}
```


## Printing and Formatting

```go
package main
import "fmt"

func main() {
    fmt.Print("xxx")
    fmt.Println("yyy")
    var name string = "aaa"
    var age int = 33
    var height float64 = 1.1
    var p *string = &name
    fmt.Printf("%s %d %f %p %b", name, age, height, p, age)
}
```


## Control structures

### If

```go
```


### For

```go
var names [3]int = [3]int{1,2,3}
var names = [...]string{"a","b","c"}
for k,v := range names {
    fmt.Println(k,v)
}
```

### Switch

```go
```


## Functions



### Defer

## Data

### Allocation with new

```go
var p *int = new(int)
fmt.Println(*p)
```

### Constructors and composite literals

### Allocation with make

```go
var s []int = make([]int, 3, 5)
//var s []string = make([]string, 3, 5)
fmt.Println(s)
```

### Arrays

```go
var arr [3]int8 = [3]int8{1,2,3}
//var arr [3]int = [3]int{1,2,3}
fmt.Printf("%p\n", &arr)
fmt.Println(&arr[0])
fmt.Println(&arr[1])
fmt.Println(&arr[2])
```

### Slices

### Two-dimensional slices

### Maps


### Append

```go
```


### The init function
```go
func init() {
    if user == "" {
        log.Fatal("$USER not set")
    }
    if home == "" {
        home = "/home/" + user
    }
    if gopath == "" {
        gopath = home + "/go"
    }
    // gopath may be overridden by --gopath flag on command line.
    flag.StringVar(&gopath, "gopath", gopath, "override default GOPATH")
}
```


## Methods

### Pointers vs. Values

```go
var x int = 10
fmt.Printf("%p\n", &x)
var p *int = &x
fmt.Printf("%p\n", &p)
fmt.Println(p)
fmt.Println(*p)
```

## Interfaces and other types

### Interfaces

### Conversions

### Interface conversions and type assertions

### Generality

### Interfaces and methods


> Reference:
> 1. [Official Website](https://go.dev)
> 2. [Repository](https://github.com/golang/go)
> 3. [Go语言中文网](https://studygolang.com/dl)
