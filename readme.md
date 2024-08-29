
# Mapper Package

The `mapper` package provides a simple utility to map data from one struct to another using JSON serialization and deserialization. This can be useful for quickly transforming one data structure into another without manually copying fields.

## Installation

To use the `mapper` package in your project, you need to have Go installed. Then, simply include the package in your project by copying the source code into a file named `mapper.go`.

## Usage

### AutoMap Function

The `AutoMap` function is the core utility provided by this package. It allows you to map data from one struct to another by converting the origin struct to JSON and then unmarshalling it into the destination struct.

#### Example:

```go
package main

import (
    "fmt"
    "github.com/byuang/mapper"


type Source struct {
    Name  string
    Age   int
    Email string
}

type Destination struct {
    Name  string
    Email string
}

func main() {
	source := Source{
		Name:  "John Doe",
		Age:   30,
		Email: "john.doe@example.com",
	}

    var destination Destination

    mapper.AutoMap(source, &destination)

    fmt.Printf("Mapped Destination: %+v\n", destination)
}
```

### StructToJson Function

The `StructToJson` function converts a struct to its JSON string representation.

#### Example:

```go
jsonStr := mapper.StructToJson(source)
fmt.Println(jsonStr)
```

### JsonToStruct Function

The `JsonToStruct` function converts a JSON string to a generic Go data structure (`interface{}`).

#### Example:

```go
jsonStr := `{"Name":"John Doe","Email":"john.doe@example.com"}`
data, err := mapper.JsonToStruct(jsonStr)
if err != nil {
    fmt.Println("Error:", err)
}
fmt.Printf("Data: %+v\n", data)
```

## Notes

- **Type Safety**: The `Mapper` function does not perform type checks, so ensure that the types of fields in the destination struct are compatible with those in the origin struct.
- **Error Handling**: The `Mapper` function does not handle errors during the unmarshalling process. In production code, consider adding error handling as needed.
- **Limitations**: The package works well for simple structs with compatible JSON tags. However, for more complex transformations, consider other mapping strategies.
