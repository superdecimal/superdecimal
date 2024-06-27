# Hello World!

```golang
package main

import (
	"fmt"
)

func main() {
	done := make(chan bool)
	hellos := make(chan string)

	go func() {
		for i := 0; i < 10; i++ {
			hellos <- "Hello World"
		}
		done <- true
	}()

	go func() {
		for {
			select {
			case hello := <-hellos:
				fmt.Println(hello)
			}
		}
	}()

	<-done
}
```
