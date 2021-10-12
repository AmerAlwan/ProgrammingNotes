# Lambdas

Lambdas are generally used to perform a short computation where writing a full-fledged function would no make sense. 

Lambdas are an anonymous that are restricted to a single expression

The general syntax for a lambda expression is:

```python
variable = lambda arguments : operations
```

## Declaring a Lambda

### Single Variable

To declare a lambda with a single variable:

```python
total = lambda a : a + 10
```

### Multiple Variables

To declare a lambda with multiple inputs, separate each variable with a comma.

```python
total = lambda a, b : a  + b
```

### Unknown Variables

To declare a lambda with multiple unknown inputs, declare one variable with `*` before it

```python
total = lambda *var : sum(var)
```

 ## Calling a Lambda

Since a lambda is essentially like a function, it can be called like a function

```python
total = lambda a, b : a + b
print(total(1,2)) # >> 3
```

## Conditional Statements

To use an `if` conditional statement, first right the action to execute followed by the condition.

### Single Condition

```python
add = lambda x : x + 1 if x == 1 else x + 2
```

### Multiple Conditions

```python
add = lambda x : x + 1 if x == 1 else x + 2 if x == 2 else x + 3
```

