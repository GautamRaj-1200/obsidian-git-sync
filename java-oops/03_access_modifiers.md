# Access Modifiers in Java
- Access modifiers in Java are the keywords that are used for controlling the use of the methods, constructors, fields, and methods in a class.

| Context\Access Modifier               | private | default (no modifier) | protected | public |
| ------------------------------------- | ------- | --------------------- | --------- | ------ |
| **Same Class**                        | Yes     | Yes                   | Yes       | Yes    |
| **Same Package**                      | No      | Yes                   | Yes       | Yes    |
| **Subclass (same package)**           | No      | Yes                   | Yes       | Yes    |
| **Subclass (different package)**      | No      | No                    | Yes       | Yes    |
| **Different Package (non-subclass)**  | No      | No                    | No        | Yes    |

## Explanation:

- **Private**: 
  - Accessible only within the same class.
  
- **Default (no modifier)**: 
  - Accessible within the same class and same package.
  
- **Protected**: 
  - Accessible within the same class, same package, and subclasses (even in different packages).
  
- **Public**: 
  - Accessible everywhere, i.e., same class, same package, subclasses, and different packages.
