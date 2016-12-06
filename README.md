test file used: https://github.com/json-iterator/test-data/blob/master/large-file.json

* jsonparser: https://github.com/buger/jsonparser
* jsoniter pull-api: https://github.com/json-iterator/go
* jsoniter reflect-api: https://github.com/json-iterator/go/blob/master/jsoniter_reflect.go
* encoding/json: golang standard lib

The goal is to prove jsoniter is not slow, not to prove it is the fastest, at least good enough.
My motivation of inventing json iterator is the flexibility to mix high level and low level api.
Performance is the by-product of schema based parsing.

* CPU: i7-4790 @ 3.6G
* Go: 1.8beta1

# small payload

| jsonparser  | jsoniter pull-api | jsoniter reflect-api | encoding/json |
| ---         | ---               | ---                  | ---           |
| 691 ns/op   | 661 ns/op         | 982 ns/op            | 4740 ns/op    |
| 64 B/op     | 64 B/op           | 256 B/op             | 864 B/op      |
| 2 allocs/op | 2 allocs/op       | 4 allocs/op          | 31 allocs/op  |

pull-api is fast, and reflect-api is not slow either.

# medium payload

| jsonparser  | jsoniter pull-api | jsoniter reflect-api | encoding/json |
| ---         | ---               | ---                  | ---           |
| 5958 ns/op  | 5662 ns/op        | 6943 ns/op           | 30902 ns/op   |
| 104 B/op    | 104 B/op          | 344 B/op             | 2168 B/op     |
| 4 allocs/op | 4 allocs/op       | 14 allocs/op         | 107 allocs/op |

again, the reflect-api is not slow