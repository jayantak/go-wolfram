# go-wolfram
Single file library for the Wolfram Alpha API written in Golang without extra dependencies

# Installing
`go get github.com/Krognol/go-wolfram`

# Example
```go
package main

import "github.com/Krognol/go-wolfram"

func main() {
	//Initialize a new client
	c := &wolfram.Client{AppID:"your app id here"}

	//Get a result without additional parameters
	res := c.GetQueryResult("1+1", nil)

	//Iterate through the pods and subpods
	//and print out their title attributes
	for i := range res.Pods {
		println(res.Pods[i].Title)

		for j := range res.Pods[i].SubPods {
			println(res.Pods[i].SubPods[j].Title)
		}
	}
}
```
### Output

```
> go run main.go

< Input
< Result
< Number name
< Visual representation
< Number line
< Illustration
```

# Adding extra parameters

```go
package main

import "github.com/Krognol/go-wolfram"

func main() {
	//Initialize a new client
	c := &wolfram.Client{AppID:"your app id here"}
  
  	params := &wolfram.AdditionalUrl{Add: []string{"DateOrder_**Day.Month.Year--"}}
  
	//Get a result without additional parameters
	res := c.GetQueryResult("26-9-2016", params)

	//Iterate through the pods and subpods
	//and print out their title attributes
	for i := range res.Pods {
		println(res.Pods[i].Title)

		for j := range res.Pods[i].SubPods {
			println(res.Pods[i].SubPods[j].Title)
		}
	}
}
```

### Output

```
> go run main.go

< Input interpretation
< Date formats
< Time difference from today (Friday, September 23, 2016)
< Time in 2016
< Observances for September 26 (Sweden)
< Anniversaries for September 26, 2016
< Daylight information for September 26 in Stockholm, Sweden
< Phase of the Moon
```
