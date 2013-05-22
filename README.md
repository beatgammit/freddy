freddy
======

Freddy extends on Go's `encoding/json` by adding support for multiple tags. I hope to get this merged into the standard library eventually.

New functions:
--------------

* MarshalTag(interface{}, ...string)- marshals a type using the specified tag(s) instead of `json`
* UnmarshalTag([]byte, interface{}, ...string)- unmarshals into a type using the specified tag(s) instead of `json`
