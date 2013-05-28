freddy [![Build Status](https://travis-ci.org/beatgammit/freddy.png)](https://travis-ci.org/beatgammit/freddy)
======

Freddy extends on Go's `encoding/json` by adding support for multiple tags. I hope to get this merged into the standard library eventually.

New functions:
--------------

* MarshalTag(interface{}, ...string)- marshals a type using the specified tag(s) instead of `json`
* UnmarshalTag([]byte, interface{}, ...string)- unmarshals into a type using the specified tag(s) instead of `json`

Tags are tried in user-defined order. The first tag that exists is used. For example:

    type Struct struct {
        A string `json:"B" api:"-" db:"a"`
        B string `json:"-" db:"b"`
    }
    func main() {
        a := A{"hi","bye"}
        json.Marshal(a) // {"B":"hi"}
        json.MarshalTag(a) // {"A":"hi","B":"bye"}
        json.MarshalTag(a, "api") // {"B":"bye"}
        json.MarshalTag(a, "db") // {"a":"hi","b":"bye"}
        json.MarshalTag(a, "api", "json") // {"B":"hi"}
    }

When using the (Un|M)arshalTag functions, the "json" tag is not automatically appended. (Un|M)arshal are just aliases that pass in "json".
