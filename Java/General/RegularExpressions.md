# Regular Expressions

### Replace vs ReplaceAll

`replaceAll()` supports regular expressions while `replace` does not.

### Is vs IsNot

To represent something that is, you write its identifier in lowercase. To represent that it is not, you write its identifier in uppercase.

Ex: 

* `d` = is integer, D = is not integer
* s = is space, S = is not space
* w = is a word character, W = not a word character

### Parenthesis & Dollar  sign

A parenthesis around anything means you are putting it in memory. A `$` will capture that item in memory. The `$` sign is proceeded by the capture number.

Ex:

* If you have `"(\\d)(\\S)"`, then doing  `"$1"` will return the value of `(\\d)` and doing `"$2"` will return the value of `(\\S)`

### Plus sign

A `+` means that there is one or more of that character.  

Ex:

* `"(\\d+)"` would get an integer with one or more digits

## Examples

### Reverse  a String of Double

To reverse a string with numbers, the item being replaced will be lowercase `\\d`, which represents Integer. An uppercase `D` would mean not an integer.

```java
"55.88".replaceAll("(\\d+)(\\S)(\\d+)", "$352$1")
```

### Parsing an Equation

```java
Matcher m = Pattern.compile("\\d+|\\S").matcher("8 * 2 + 3");
while(m.find()) {
    lst.add(m.group());
}
```

