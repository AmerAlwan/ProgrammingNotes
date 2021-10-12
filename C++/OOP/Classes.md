# Classes

## Class Files

Classes in C++ can have two files associated with each class:

- The Interface file (*.h)
- The implantation file (*.cpp)

### Interface File Example

```c++
//
// class rational - rational number data abstraction
//
class rational {
public:
    //constructors
    rational    ();
    rational    ( int );
    rational    ( int, int );
    rational    ( const rational & );

    //accessor functions
    int         numerator () const;
    int         denominator () const;

    //assignments
    void        operator =  ( const rational & );
    void        operator += ( const rational & );

private:
    //data areas
    int         top;
    int         bottom;

    //operation used internally
    void        normalize ();
}
```

## Member vs Non-Member Functions

### Inside a Class

#### 	Member Function	

> ```c++
> int exampleFunction() 
> ```

#### 	Non-Member Function

Although it can be declared inside the class, a `friend` function can be defined outside of the class but still be able to acces sprotected and private items of the class

> ```c++
> friend int exampleFunction()
> ```

### Outside a Class

#### 	Member Function	

> ```c++
> //exampleFunction must declared inside of ExampleClass
> int ExampleClass::exampleFunction() 
> ```

#### 	Non-Member Function

> ```c++
> int exampleFunction()
> ```

## Const

There are 3 placements of `const` in C++:

### 	Before Function 

​	This entails that the returned variable will be a constant

> ```c++
> const int exampleFunction()
> ```

### 	After Function

​	Declares that no variables inside the function will be created or changed

> ```c++
> int exampleFunction() const
> ```

### 	Before Variables

​	The variables which are declared with `const` cannot be changed

> ```c++
> int exampleFunction(const int exampleVariable)
> ```

