# Reflect

## Basic

* Any var of interface is a pair `(value, type)`
* Get value by `reflect.ValueOf(i interface) reflect.Value`
  * Get value for a known type `reflect.Value.Interface().(known_type)`
* Get type by `reflect.TypeOf(i interface) reflect.Type`
* Loop fields
  * `reflect.Type.NumField()` and `reflect.Type.Field(int)`
  * `reflect.Type.NumMethod()` and `reflect.Type.Method(int)`
* Only addressable values got by `reflect.ValueOf(*ptr)` can be modified
* Call method via reflect

```go
reflect.Value := reflect.ValueOf(interface{})
# method := reflect.Value.Method(int)
method := reflect.MethodByName(string)
[]reflect.Value{} := method.Call([]reflect.Value{})
```

## Example

```go
package main

import (
	"fmt"
	"reflect"
)

// Person ...
type Person struct {
	Name string
	Age  int
}

func main() {
	p := &Person{
		Name: "hello",
		Age:  100,
	}

	pt := reflect.ValueOf(p).Elem()

	for i := 0; i < pt.NumField(); i++ {
		f := pt.Field(i)
		t := pt.Type().Field(i)
		if t.Type.Kind() == reflect.String {
			fmt.Printf("%s=%v\n", t.Name, f.Interface())
		}
	}

}

```
