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

jump back: `Alt + -`

jump forward: `Alt + Shift + -`

upper case: `Ctrl + KU`

lower case: `Ctrl + KL`

[referece](https://gist.github.com/mrliptontea/4c793ebdf72ed145bcbf)

[//]: # (go to method:<kbd>Ctrl</kbd>+<kbd>R</kbd>)

### Environment Setting

#### Set Python3 Build

step 1:
In sublime text 3, select `Tools -> Build System -> New Build System`

step 2: 
find your python3 path, maybe you can use `which` command to find.

```console
$ which python3
```
in my case, my path is */usr/bin/python3*

step 3:
then, add following code:
```plain
{
 "cmd": ["/usr/bin/python3", "-u", "$file"],
 "file_regex": "^[ ]File \"(...?)\", line ([0-9]*)",
 "selector": "source.python"
}
```

step 4:
save as: `py3.sublime-build`

step 5:
select, `Tools -> Build System -> py3`

and run your code using `Ctrl+B`

## Vim 

### shortcut key

Delete character: `x`

go to 2nd line: `:2`

add: `a` or `A`

move down: `j`

move up: `k`

move left: `h`

move right: `l`

go bottom: `G`

go top: `gg`

add a line(below): `o`

add a line(above): `O`

go to next word: `w`

go back last word: `b`

delete word: `dw`

delete rest of line: `D`

delete rest of line and insert: `C`

deletl to char a: `dta`



## Go 

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
