### Tour de Go 
[link](https://tour.golang.org)

#### Imports
***
##### Tips
* Is good style to use the factored import statement

#### Exported Names
***

##### Tips
* Any "unexported" names are not visible from the outside the package

#### Functions
***

##### Tips
* You can ommit the type from all parameters but the last, when un have a function with same parameters
* A function can return any number of results
* A return statement without arguments returns the named return values, this should be used only in short functions [link](https://tour.golang.org/basics/7)
* 

#### Variables
***

##### Tips
* A var statement can be at package or function level
* If initializer is present the type can be omitted
* variables declared without an explicit initial value are given their zero value (string ==> '' empty - int ==> 0 - bool ==> false)


#### Constants
***

##### Tips
* Constants cannot be declared using the := syntax

#### Loops - For
***

##### Tips
* Go has only one looping construct
* Init and post statements are optional [link](https://tour.golang.org/flowcontrol/2)
* If you omit loop condiction it loops forever

#### Loops & Functions Exercise
```go 
package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	//z := 1.0
	z := float64(1)

	for i := 0; i < 10; i++ {
		z -= (z*z - x) / (2 * z)
	}
	return z
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(math.Sqrt(2))
}

```

#### If Else
***

##### Tips
* Variables declared inside an if are also available inside any of the else blocks


#### Switch
***

##### Tips
* Cases need not be constants, and the values involved need not be integers
* Switch without condiction is the same true [link](https://tour.golang.org/flowcontrol/11) to avoid long if else chains

#### Defer
*** 

##### Tips
* A defer statement defers the execution of a function until the surrounding function returns.[link](https://tour.golang.org/flowcontrol/12)

#### Pointers
*** 

##### Tips
* Its zero value is nil
* The & operator generates a pointer to its operand

#### Structs
*** 

##### Tips
* Is a collections of fields

#### Arrays
*** 

##### Tips
* Arrays cannot be resized

#### Slices
*** 

##### Tips
* Is a dynamically sized, is like an array without the lenght
* Slice lenght len(x) return number of elements it contains
* Slice cap cap(x) is the number of elementes in the underlying array
* The zero value of a slice is nil
* A slice can be inside another slice

#### Range
*** 

##### Tips
* Using range to iterate over array or slice, the fisrt is the index and the second is a copy of the element

#### Maps
*** 

##### Tips
* The zero value of map is nil

#### Functions
*** 

##### Tips
* Can sended by arguments inside another functions [link](https://tour.golang.org/moretypes/24)
* Using T type fn in the func signature

#### Fibonacci Exercise
*** 
``` go 
package main
import "fmt"
func fibonacci() func(int) int {
	prevNumber := 0
	nextNumber := 1

	return func(x int) int {
  // lo comentado es programado por mi
		/*if x < 2 {
			nextNumber = x
			prevNumber = x - 1

			return x
		}*/

		f := prevNumber
		prevNumber, nextNumber = nextNumber, nextNumber+prevNumber
		//f := prevNumber + nextNumber

		//prevNumber = nextNumber
		//nextNumber = f

		return f
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Print(" ", f(i))
	}
}
```

#### Methods
*** 

##### Tips
* Go does not have classes
* A method is just a function that recive arguments

#### Pointer Receiver
*** 

##### Tips
* When we send a struct to a receiver (functions) it makes a copy of the struct and operate it, but if the funciton receive has a syntax *T where it is a pointer the receive will mofify the struct values
* For the statement v.Scale(5), even though v is a value and not a pointer, the method with the pointer receiver is called automatically. That is, as a convenience, Go interprets the statement v.Scale(5) as (&v).Scale(5) since the Scale method has a pointer receiver [link](https://tour.golang.org/methods/6)
* The first is so that the method can modify the value that its receiver points to.
* The second is to avoid copying the value on each method call. This can be more efficient if the receiver is a large struct, for example.

#### Interfaces
*** 

##### Tips
* Is defined as a set of method signatures
* If the concrete value inside the interface itself is nil, the method will be called with a nil receiver.

#### Nil Interfaces Values
*** 

##### Tips
* Calling a method on a nil interface is a run-time errorbecause there is no type inside

#### Empty Interfaces
*** 

##### Tips
* Are used by code that handles values of unknown type [link](https://tour.golang.org/methods/14)

#### Type Assertions
*** 

##### Tips
* Provides access to an interfaces value's underlying concrete value t, ok := i.(T) [link](https://tour.golang.org/methods/15)

#### Type Switches
*** 

##### Tips
* Allow several type aseertions in series
* You can specify types in the case statements [link](https://tour.golang.org/methods/16)
* Show *type assertions

#### Stringers
*** 

##### Tips
* Is an interface from fmt thatg describe itself as string, you can use it to override print lines[link](https://tour.golang.org/methods/17)

#### Stringers Exercise
*** 
``` go 
package main

import "fmt"
//import "strconv"

type IPAddr [4]byte

// TODO: Add a "String() string" method to IPAddr.

func (ipAddr IPAddr) String() string {
	data := ""
	for i, v := range ipAddr {
		if (i < 1) {
			data = data + fmt.Sprintf("%v", v)
		}else {
			data = data + fmt.Sprintf(".%v", v)
		}
	}

	return fmt.Sprintf("\"%v\"", data)
}

func main() {
	hosts := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}

	for _, ip := range hosts {
		fmt.Println(ip)
	}
}
```

#### Errors
*** 

##### Tips
* The error type is a built-in interface similar to Stringer
* A nil error denotes success

#### Errors Exercise
*** 
