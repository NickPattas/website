*A pointer is a variable* that holds the **memory address** of another variable, allowing direct manipulation of memory addresses.

Using pointers significantly *improves performance* for repetitive operations, like traversing iterable data structures (e.g. strings, lookup tables, control tables, linked lists, and tree structures). In particular, it is often much cheaper in time and space to copy and dereference pointers than it is to copy and access the data to which the pointers point.

A pointer is a `simple`, `more concrete` implementation of the more *abstract [[Reference]] data type*. Several languages, especially *low-level languages*, support some type of pointer, although some have more restrictions on their use than others.

While "pointer" has been used to refer to references in general, it more properly applies to data structures whose **interface explicitly allows the pointer to be manipulated** as a memory address, as opposed to a [[Magic Cookie]] or [[Capability]] which *does not allow such*. Because pointers allow both **protected and unprotected access to memory addresses**, there are risks associated with using them, particularly in the latter case.

**Primitive pointers** are often stored in a format similar to an integer; however, attempting to dereference or "look up" such a pointer whose value is not a valid memory address could cause a program to **crash** (or contain invalid data). To alleviate this potential problem, as a matter of type safety, pointers are considered a separate type parameterized by the type of data they point to, even if the underlying representation is an integer.

Other measures may also be taken (such as validation and bounds checking), to verify that the pointer variable contains a value that is both a valid memory address and within the numerical range that the processor is capable of addressing.

---

In C and C++ **Asterisk or Start** (`*`) is the **dereferencing operator**. Using this operator accesses the value at the address pointed to by a pointer.

Operations like incrementing a pointer move it to the next memory address, useful for traversing arrays or linked lists.

Pointers are used to pass variables by reference, allowing functions to modify original data directly and efficiently.

Each pointer type must point to a specific data type (e.g., integer vs. character), preventing type mismatches.

**Safety Considerations**
 Misusing pointers can lead to issues like buffer overflows or null dereferences, emphasizing the need for careful handling.
 Pointers provide **low-level control** over memory but require **careful management to avoid errors.**

---
#### Null Pointers
A **null pointer** refers to a reference variable that does not point to any object or array. Attempting to use such a reference results in a **NullPointerException**, which is a common runtime error.

- A null pointer is a variable of reference type (e.g., `String`, `Object[]`) that holds the special value `null`.
- Operations on a null pointer, like calling methods or accessing fields, will throw a `NullPointerException`.

 #### C++
  A pointer in C++ must be assigned a valid memory address or set to `nullptr`. Accessing memory through an uninitialized or null pointer results in undefined behavior.

 #### C
  In C, a null pointer is represented by the macro `NULL`, which is defined as a pointer to a special null object. Like C++, accessing memory through a null pointer in C leads to undefined behavior.

 #### Python
  In Python, the concept of "null" is represented by the special value `None`. Unlike C++ or C, Python **does not have pointers in the traditional sense** because it uses [[Reference]] Counting for memory management.