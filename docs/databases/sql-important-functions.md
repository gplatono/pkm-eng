# List of important SQL functions:

### `CAST(expresion AS datatype)`

CAST converts the *expression* into a *datatype*. 
```
Example: CAST(12 as varchar) returns "12"
```

### `SUBSTR (STRING, POSITION, LENGTH)`

Extracts and returns a substring of a string `STRING`, starting from index `POSITION` and taking `LENGTH` characters. The string is indexed starting from 1.
```
Example: SUBSTR('substr test', 1, 6) -> 'substr'
```