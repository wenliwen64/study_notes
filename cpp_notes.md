# C++ Notes



### Type Conversion

* Narrower than int, promote it to int
* Otherwise, implicit conversion to highest operand priority type:
  * long double(8 bytes or more)
  * double (8 bytes)
  * float(4 bytes)
  * unsigned long long (8 bytes)
  * long long (8 bytes)
  * usigned long(4 bytes)
  * long (4 bytes)
  * unsigned int (4 bytes)
  * int(4 bytes, depends)
* Two different type conversion? 
  * Implicit type conversion
  * Explicit type conversion:
    * c-style type cast(dangerous , ex. `float(8)`, dont check in compile time, so it may not make any sense), could be complicated, you dont know which type is it going to do
    * static_cast(compile time, used to convert one fundamental type into another): also can do the conversions between pointers to related classes. but no check is done in runtime, dynamic_cast would do this and incur type check overhead. 
    * dynamic_cast: type conversion between pointers or reference to Classes, its purpose is to ensure that the result of type conversion points to a valid complete object of the destination pointer type, so it allows upcast (derived to base) and downcast(base to derived)
    * const_cast: cast away const/volatile
    * reinterpret_cast: even between unrelated classes