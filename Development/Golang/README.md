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


## 3. Training

### Basic grammar

#### Commentary

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

#### Constants
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

#### Variables
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

#### Operator
```go
// arithmetic
+
-
*
/
%

// relational
x == x
x != x
>
<
>=
<=

// logical
x && y
x || y
!(x < 18)

// assignment
x = 1
x += 1
x -= 1
x *= 1
x /= 1
x %= 1
x <= 1
x >= 1
x &= 1
x ^= 1
x |= 1
```


#### Printing and Formatting

```go
/*
    %s    string
    %d    decimal integer
    %f    floating-point number
    %b    binary
    %o    octal
    %x    hexadecimal(lowercase)
    %X    hexadecimal(uppercase)
    %v    default format
    %T    typeof variable
    %p    pointer address
*/
// Print, Println
fmt.Print("xxx")
fmt.Println("yyy")

var name string = "logic"
var age int = 33
var height float64 = 1.1
var p *string = &name
// Printf, Sprintf
fmt.Printf("%s %d %f %p %b", name, age, height, p, age)
s := fmt.Sprintf("%s %d %f %p %b", name, age, height, p, age)
fmt.Println(s)

var (
    name     string
    age      int
    married  bool
)
// Scan, Scanf, Scanln
fmt.Scan(&name, &age, &married)
fmt.Scanf("1:%s 2:%d 3:%t", &name, &age, &married)
fmt.Scanln(&name, &age, &married)
//
fmt.Printf("name:%s age:%d married:%t", name, age, married)
```

### Data type

#### bool
```go
var b1 = true
var b2 = false
fmt.Println(reflect.TypeOf(b1), reflect.TypeOf(b2))
```

#### float
```go
var f1 float32 = 3.1234567890123456789
f1 = 2e10
fmt.Println(f1, reflect.TypeOf(f1))

var f2 float64 = 3.1234567890123456789
f2 = 2e-2
fmt.Println(f2, reflect.TypeOf(f2))
```

#### int
```go
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
```

#### string
```go
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
multi line one
multi line two
`
fmt.Println(s1, s2, s3)


// strings method
fmt.Println(strings.ToUpper(s))
fmt.Println(strings.ToLower(s))
fmt.Println(strings.TrimLeft(s, ""))
fmt.Println(strings.Trim(s, ""))
fmt.Println(strings.Index(s, "world"))
fmt.Println(strings.HasPrefix(s, "hello"))
fmt.Println(strings.Contains(s, "llo"))
fmt.Println(strings.Join([]string{"a","b","c"}, ","))

// strconv method
// int to int
i = 100
fmt.Println(int64(i), reflect.TypeOf(int64(i)))
fmt.Println(float64(i), reflect.TypeOf(float64(i)))
// int to string
x := strconv.Itoa(98)
fmt.Println(x, reflect.TypeOf(x))
// string to int
y, _ := strconv.Atoi("97")
fmt.Println(y, reflect.TypeOf(y))
i1, _ := strconv.ParseInt("1000", 10, 8)
println(i1)
i2, _ := strconv.ParseInt("1000", 10, 64)
println(i2)
// string to float
f2, _ := strconv.ParseFloat("3.1415926", 64)
fmt.Println(f2, reflect.TypeOf(f2))
f1, _ := strconv.ParseFloat("3.1415926", 32)
fmt.Println(f1, reflect.TypeOf(f1))
// string to bool
b1, _ := strconv.ParseBool("true")
fmt.Println(b1, reflect.TypeOf(b1))
b2, _ := strconv.ParseBool("T")
fmt.Println(b2, reflect.TypeOf(b2))
b3, _ := strconv.ParseBool("1")
fmt.Println(b3, reflect.TypeOf(b3))
b4, _ := strconv.ParseBool("100")
fmt.Println(b4, reflect.TypeOf(b4))
```

#### pointer
```go
/*
    &  address character,return address
    *  value character, return value
*/
// example
var i = 100
fmt.Println("i address:", &i)
fmt.Println("i value:", i)
var p *int
p = &i
fmt.Println("p address:", &p)
fmt.Printf("p address: %p\n", &p)
fmt.Println("p value:", p)
fmt.Println("p value's address's value:", *p)
fmt.Println(*&p)

// **p
var a = 100
var b = &a
var c = &b
**c = 200
fmt.Println(a)

// new function, allcated memory
var p *int = new(int)
fmt.Println(p)
fmt.Println(*p)
```


#### array
```go
// example
var arr = [3]int8{1,2,3}
fmt.Printf("%p\n", &arr)
fmt.Println(&arr[0])
fmt.Println(&arr[1])
fmt.Println(&arr[2])

// infinity array
var names = [...]string{"alice","bob","candy"}
fmt.Printf("%p\n", &names)
fmt.Println(&names[0])
// get element
fmt.Println(names[0])
// modify element
names[0] = "logic"
// slice
fmt.Println(names[0:2])
// range
for k,v := range names {
    fmt.Println(k,v)
}
```

#### slice
```go
/*
type Slice struct {
      Data uintptr   // 指针，指向底层数组中切片指定的开始位置
      Len int        // 长度，即切片的长度
      Cap int        // 最大长度（容量），也就是切片开始位置到数组的最后位置的长度 
}
*/
// option1: from array
var arr = [5]int{10, 11, 12, 13, 14} 
sa := arr[1:2]

// option2: declare variable, not allocated memory
var sv []string{}

// option3: make([]Type, size, cap), allocated memory
var sm = make([]string, 3, 5)


// address check
var arr = [5]int{10, 11, 12, 13, 14}  // int64 = 8Bytes
s1 := arr[0:3] // 对数组切片
s2 := arr[2:5]
s3 := s2[0:2] // 对切片切片

fmt.Println(s1) // [10, 11, 12]
fmt.Println(s2) // [12, 13, 14]
fmt.Println(s3) // [12, 13]

// 地址是连续的
fmt.Printf("%p\n", &arr)
fmt.Printf("%p\n", &arr[0]) // 相差8个字节
fmt.Printf("%p\n", &arr[1])
fmt.Printf("%p\n", &arr[2])
fmt.Printf("%p\n", &arr[3])
fmt.Printf("%p\n", &arr[4])

// 每一个切片都有一块自己的空间地址，分别存储了对于数组的引用地址，长度和容量
fmt.Printf("%p\n", &s1) // s1自己的地址
fmt.Printf("%p\n", &s1[0])
fmt.Println(len(s1), cap(s1))

fmt.Printf("%p\n", &s2) // s2自己的地址
fmt.Printf("%p\n", &s2[0])
fmt.Println(len(s2), cap(s2))

fmt.Printf("%p\n", &s3) // s3自己的地址
fmt.Printf("%p\n", &s3[0])
fmt.Println(len(s3), cap(s3))


// append, extend slice
var emps = make([]string, 3, 5)
emps[0] = "aaa"
emps[1] = "bbb"
emps[2] = "ccc"
fmt.Println(emps)
emps2 := append(emps, "ddd")
fmt.Println(emps2)
emps3 := append(emps2, "eee")
fmt.Println(emps3)
// 容量不够时默认发生二倍扩容
emps4 := append(emps3, "xxx")
fmt.Println(emps4, len(emps4), cap(emps4)) // 此时底层数组已经发生变化

// append element
append(emps, "xxx", "yyy")
// apend a slice
append(emps, []string{"A","B","C"}...)

// delete element
append(emps[:1], emps[2:]...)

// sort
si := []int{3,5,1}
sort.Ints(si)
ss := []string{"melon","banana","apple"}
sort.Strings(ss)
sf := []float64{3.14,5.25,1.12,4,78}
sort.Float64s(sf)

// copy
var s1 = []int{1, 2, 3, 4, 5}
var s2 = make([]int, len(s1))
copy(s2, s1)
fmt.Println(s2)
s3 := []int{4, 5}
s4 := []int{6, 7, 8, 9}
copy(s4, s3)
fmt.Println(s4)
```

#### map
```go
/*
type hmap struct { 
    count     int // 当前 map 中元素数量 
    flags     uint8 
    B         uint8  // 当前 buckets 数量，2^B 等于 buckets 个数 
    noverflow uint16 // approximate number of overflow buckets; see incrnoverflow for details 
    hash0     uint32 // 哈希种子 

    buckets    unsafe.Pointer // buckets 数组指针 
    oldbuckets unsafe.Pointer // 扩容时保存之前 buckets 数据。 
    nevacuate  uintptr        // progress counter for evacuation (buckets less than this have been evacuated) 

    extra *mapextra // optional fields 
} 
*/
// option1: declare
var m map[string]string
m["name"] = "logic"

// option2: declare
m := map[string]string{"name": "logic"}

// option3: make(map[keytype]valuetype, cap)
m := make(map[string]string, 10)
fmt.Println(m, len(m))


// select 
for k,v := range m {
    fmt.Println(k,v)
}

// add and delete
m["new_key"] = "new_value"
delete(m, "name")
```

#### channel
```go
/*
*/

```


### Control structures

#### if
```go
// if
if true {
    // do something
}

// if, else
score := 33
if score < 10 {
    fmt.Println("less than 10")
} else {
    fmt.Println("greater than 10")
}

// if, else if, else
if score < 10 {
    fmt.Println("less than 10")
} else if score < 20 {
    fmt.Println("less than 20")
} else {
    fmt.Println("greater than 20")
}
```

#### switch
```go
choice := "fff"
switch choice {
    case "a":
        fmt.Println("a")
    case "b":
        fmt.Println("b")
    case "x", "y":
        fmt.Println("xy")
    default:
        fmt.Println("x")
}
```

#### for
```go
// option1
count := 0
for count < 10 {
    fmt.Println(count)
    // count ++
    count += 1
}

// option2
for i:=1; i<10; i++ {
    if i % 2 == 0{
        fmt.Println(i)
    } else if i == 6 {
        continue
    } else if i == 7 {
        break
    }
}

// option3
var names [3]int = [3]int{1,2,3}
var names = [...]string{"a","b","c"}
for k,v := range names {
    fmt.Println(k,v)
}
```

### Functions

#### Example
```go
/*
func FunctionName(p1 paramType, p2 paramType) (returnType, returnType) {
    doSomething...
    return r1, r2
}
*/

// positional parameter
func add_cal(x int, y int) {
    fmt.Pringln(x+y)
}

// indefinite length parameter
func sum(nums ...int) {
    for _, num := range nums {
        fmt.Println(num)
    }
}

// return value
func get_name_age() (string, int) {
    return "logic", 99
}
func calc(x, y int) (sum, sub int) {
    sum = x + y
    sub = x - y
    return     //  return sum sub
}
```

#### Pass-by-xxx
```go
/* 
Pass-by-value
    @int
    @string
    @struct

Pass-by-reference
    @pointer
    @slice
    @map
    @chan
*/
func func01(x int) {
    x = 100
}
func func02(s []int) {
    fmt.Printf("func02 var s address: %p\n",&s)
    s[0] = 100
    // s = append(s, 1000)
}

func func03(p *int)  {
    *p = 100
}
func main() {
    // example1
    var x = 10
    func01(x)
    fmt.Println(x)

    // example2
    var s = []int{1, 2, 3}
    fmt.Printf("main var s address: %p\n",&s)
    func02(s)
    fmt.Println(s)

    // example3
    var a = 10
    var p *int = &a
    func03(p)
    fmt.Println(a)
}
```

#### anonymous function
```go
func main() {
    var c = (func(x,y int) int {
        return x + y
    })(1,2)
    fmt.Println(c)
}
```

#### higher-order function
```go
// function parameter
func add(x,y int) int {
    return x+y
}
func mul(x,y int) int {
    return x*y
}
func cal(f func(x,y int) int, x,y int) int {
    return f(x,y)
}
func main() {
    ret1 := cal(add,12,3)
    fmt.Println(ret1)
    ret2 := cal(mul,12,3)
    fmt.Println(ret2)
}
// function return
func foo() func() {
    inner := func() {
        fmt.Println("inner running..")
    }
    fmt.Println("outer running..")
    return inner
}
func main() {
    foo()()
}
```

#### closure
```go
// example1
func getCounter(f func()) func() {
    calledNum := 0
    return func() {
        f()
        calledNum += 1
        fn := runtime.FuncForPC(reflect.ValueOf(f).Pointer()).Name()
        fmt.Printf("function %s called by number %d\n", fn, calledNum)
    }
}

func foo() {
    fmt.Println("foo running")
}
func bar() {
    fmt.Println("bar running")
}

func main() {
    foo := getCounter(foo)
    foo()
    foo()
    foo()

    bar := getCounter(bar)
    bar()
    bar()
}


// example2
func GetTimer(f func(t time.Duration)) func(t time.Duration) {
    return func(t time.Duration) {
        t1 := time.Now().Unix()
        f(t)
        t2 := time.Now().Unix()
        fmt.Println("function duration: ", t2-t1)
    }
}

func foo(t time.Duration) {
    fmt.Println("foo start")
    time.Sleep(time.Second * t)
    fmt.Println("foo end")
}

func bar(t time.Duration) {
    fmt.Println("bar start")
    time.Sleep(time.Second * t)
    fmt.Println("bar end")
}

func main() {
    var foo = GetTimer(foo)
    foo(3)
    var bar = GetTimer(bar)
    bar(2)
}
```


#### defer
```go

```


#### init function
```go
func init() {
    // init log
    // init config

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
func main(){
    fmt.Println("xxx")
}
```


> Reference:
> 1. [Official Website](https://go.dev)
> 2. [Repository](https://github.com/golang/go)
> 3. [Go语言中文网](https://studygolang.com/dl)
