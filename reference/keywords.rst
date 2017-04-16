=================
PythoniC Keywords
=================

PythoniC Part
-------------

======== ============================================ ============================================
Keyword  Description                                  Example
======== ============================================ ============================================
and      Logical and.                                 ``True and False == False``
break    Stop this loop right now.                    ``while True: break``
**bool** Boolean type
class    Define a class.                              ``class Person(object)``
continue Don't process more of the loop, do it again. ``while True: continue``
def      Define a function.                           ``def X(): pass``
elif     Else if condition.                           ``if: X; elif: Y; else: J``
else     Else condition.                              ``if: X; elif: Y; else: J``
for      Loop over a collection of things.            ``for X in Y: pass``
from     Include header from subdirectory.            ``from foo import bar``
is       Same as ``==``                               ``a = 1; a is 1 == True``
if       If condition.                                ``if: X; elif: Y; else: J``
import   Include header                               ``import stdio``
in       Part of for-loops. Also a test of X in Y.    ``for X in Y: pass`` also ``1 in [1] == True``
lambda   Create a short anonymous function.           ``s = lambda y: y ** y; s(3)``
not      Logical not.                                 ``not True == False``
or       Logical or.                                  ``True or False == True``
pass     Do nothing                                   ``def empty(): pass``
print    Print this string.                           ``print("Hello")``
return   Exit the function with a return value.       ``def X(): return Y``
while    While loop.                                  ``while X: pass``
======== ============================================ ============================================

C Part
------
======== ====== ======== =======
auto     double int      struct
break    else   long     switch
case     enum   register typedef
char     extern return   union
const    float  short    unsigned
continue for    signed   void
default  sizeof volatile goto
do       if     static   while
======== ====== ======== =======

``goto`` is no longer supported in `PythoniC`, but it still is a part of `PythoniC` keywords.
