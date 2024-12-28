- In interactive mode, the last printed expression is assigned to the variable `_`. 
- In addition to int and float, Python supports other types of numbers, such as Decimal and Fraction.


### Text
- Python can manipulate text (represented by type str, so-called “strings”) as well as numbers.
- Strings can be enclosed in single quotes ('...') or double quotes ("...") with the same result.
- String literals can span multiple lines. One way is using triple-quotes: `'''...'''` or `"""..."""`. 
- Two or more string literals (i.e. the ones enclosed between quotes) next to each other are automatically concatenated.
for example, `'Py' 'thon'` is equivalent to `'Python'`.
- Strings can be indexed (subscripted), with the first character having index 0. Indices may also be negative numbers, 
to start counting from the right. For example in string `'Python'`, `P` is at index 0, `y` is at 1, `o` is at 4 and so on.
- Slicing allows you to obtain a substring: `str[0:2]` is `'Py'`.
- Strings are immutable, which means they cannot be changed.
- The built-in function `len()` returns the length of a string. e.g. `len('Python')` returns 6.

### Lists
- Python knows a number of compound data types, used to group together other values. The most versatile is the list,
which can be written as a list of comma-separated values (items) between square brackets. Lists might contain items of
different types, but usually the items all have the same type.
E.g `squares = [1, 4, 9, 16, 25]`, `squares` is a list of integers. 
- When you assign a list to a variable, the variable refers to the existing list. Any changes you make to the list 
through one variable will be seen through all other variables that refer to it.

