# VB6JSON

JSON parser/exporter for Visual Basic 6.0

## Usage

Copy `modJson.bas` to your project.

Call `ParseJSONString()` function to parse a JSON string, then get a `Variant` which represents the JSON data.
Or optionally there's another sub `ParseJSONString2()` uses a `ByRef` param to retrieve the parsed object, which helps with VB6's `Set` mess.

The returned `Variant` represents the JSON data. During parsing, the library has the following behavior:
 * Numbers turns into `Long` or `Currency` depends on it's range (i.e. If it can't fit into a `Long` then it's a `Currency`).
   - Floating point numbers or numbers with scientific notation will be a `Double`.
 * Strings turns into VB6 Strings.
 * Arrays turn into VB6 Variant Arrays, every element of the array doesn't need to be the same type.
 * Objects turns into `Scripting.Dictionary`.

The function `JSONToString()` do the reverse work: turn the `Variant` into a JSON string.

### Note

Because `Scripting. Dictionary` is a VB object but the others are not, and in VB6, assignments on objects need a `Set` syntax. Still, assignments on non-object variables need not use `Set` syntax, it's recommended not to design functions that return the data from `ParseJSONString()` or `ParseJSONString2()`, but design functions or subs that return data via params.

Use `IsObject()` to check if the `Variant` is an object, use `IsArray()` to check if if the `Variant` is an array.
Use `VarType()` to get the type of `Variant`, if the type is `vbString`, then the `Variant` is a string.
If it's not an object, nor an array, also not a string, then use `IsNumeric()` to check if it's a number.

## References

See [JSON Specification](https://www.json.org/json-en.html)

See [VarType](https://learn.microsoft.com/en-us/office/vba/language/reference/user-interface-help/vartype-function)
