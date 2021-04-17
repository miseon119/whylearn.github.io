---
sort: 5
---

# Tool

## sublime text 3

### shortcut key

Show/Hide sidebar: `Ctrl + K` and `Ctrl + B`

Duplicate lines: `Ctrl + Shift + D`

Goto line number: `Ctrl + G`

select word: `Ctrl + D`

select all of the word: `Alt + F3`

# Go 

Variable Declaration
```go
	var i int =10
	fmt.Printf("%v, %T\n", i, i)
```
or
```go
    i:=10
```

> Can't redeclare variables, but can shadow them
> variables must be used

Const
```go
	const a = 10
```
or
```go
const (
    a = 1
    b = 2 
    c = 3 
)
```

Array
```go
grades := [3]int{100, 60, 70}
fmt.Printf("grade: %v", grades)
```
or
```go
var names [3]string
names[0] = "Tim"
names[1] = "Tom"
names[2] = "Bob"
```

2D Array
```go
var mask [3][3]int
mask[0] = [3]int{1,0,1}
mask[1] = [3]int{0,1,0}
mask[2] = [3]int{0,0,1}
```
