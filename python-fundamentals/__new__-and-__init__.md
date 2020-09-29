# \_\_new\_\_ & \_\_init\_\_

## Usage

Use **`__new__`** when you need to control the creation of a new instance.  
Use **`__init__`** when you need to control initialization of a new instance.

## Difference

* **`__new__`** is the first step of instance creation. It's called first, and is responsible for returning a new instance of your class.
* **`__init__`** doesn't return anything; it's only responsible for initializing the instance after it's been created.
* **`__new__`** is static class method
* **`__init__`** is instance method

## Example A

```python
class A(object): 
    def __new__(cls): 
         print("Creating instance") 
         return super(A, cls).__new__(cls) 
  
    def __init__(self): 
        print("Init is called") 
  
A() 
```

```python
# Output

Creating instance
Init is called
```

## Example B

```python
class A(object): 
    def __new__(cls): 
        print("Creating instance") 
  
    # It is not called 
    def __init__(self): 
        print("Init is called") 
  
print(A()) 
```

```python
# Output
Creating instance
None
```

  
  


