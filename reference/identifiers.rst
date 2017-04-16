====================
PythoniC Identifiers
====================

`PythoniC` Identifiers are the same as `C` Identifiers.

"Identifiers" or "symbols" are the names you supply for variables, types,
functions, and labels in your program. Identifier names must differ in spelling
and case from any keywords. You cannot use keywords as identifiers;
they are reserved for special use. You create an identifier by specifying it in
the declaration of a variable, type, or function. In this example, `result` is
an identifier for an integer variable, and `main` and `print` are identifier names for functions.

C code

.. code-block:: c

  #include <stdio.h>

  int main() {
      int result;
      if(result != 0) {
          printf( "Bad file handle\n" );
      }
      return 0;
  }

PythoniC Code

.. code-block:: python

  import stdio

  def main() -> int:
      int result
      if result != 0:
          print( "Bad file handle" )
      return 0

Once declared, you can use the identifier in later program statements to refer to the associated value.
