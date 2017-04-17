=========================
PythoniC Lexical Analysis
=========================

PythoniC learn from Python's design ideas, as much as possible to implement
similar designs with Python on the premise of guaranteeing usability.

Encoding
========

Considering the compatibility, donnot put non-ASCII characters in your source
code (except for comments). **The default encoding is UTF-8.**

Comment for encding declarations isn't supported. If the file cannot be decoded,
an ``Encoding Error`` will be throw out.

Line structure
==============

A PythoniC program is divided into a number of logical lines.

Logical lines
-------------

The end of a logical line is represented by the token NEWLINE.  Statements
cannot cross logical line boundaries except where NEWLINE is allowed by the
syntax (e.g., between statements in compound statements). A logical line is
constructed from one or more *physical lines* by following the explicit or
implicit *line joining* rules.

Physical lines
--------------

A physical line is a sequence of characters terminated by an end-of-line
sequence.  In source files, any of the standard platform line termination
sequences can be used - the Unix form using ASCII LF (linefeed), the Windows
form using the ASCII sequence CR LF (return followed by linefeed), or the old
Macintosh form using the ASCII CR (return) character.  All of these forms can be
used equally, regardless of platform.

Comments
--------

A comment starts with a hash character (``#``) that is not part of a string
literal, and ends at the end of the physical line.  A comment signifies the end
of the logical line unless the implicit line joining rules are invoked. Comments
are ignored by the syntax; they are not tokens.

Specially, C style comment is not supported in PythoniC. Including single line
comment (``//``) and multiline comment (``/* */``).

Explicit line joining
---------------------

Two or more physical lines may be joined into logical lines using backslash
characters (``\``), as follows: when a physical line ends in a backslash that is
not part of a string literal or comment, it is joined with the following forming
a single logical line, deleting the backslash and the following end-of-line
character.  For example:

.. code-block:: python

  if 1900 < year < 2100 and 1 <= month <= 12 \
    and 1 <= day <= 31 and 0 <= hour < 24 \
    and 0 <= minute < 60 and 0 <= second < 60:   # Looks like a valid date
      return 1

A line ending in a backslash cannot carry a comment.  A backslash does not
continue a comment.  A backslash does not continue a token except for string
literals (i.e., tokens other than string literals cannot be split across
physical lines using a backslash).  A backslash is illegal elsewhere on a line
outside a string literal.

Blank lines
-----------

A logical line that contains only spaces, tabs, formfeeds and possibly a
comment, is ignored (i.e., no NEWLINE token is generated).  During interactive
input of statements, handling of a blank line may differ depending on the
implementation of the read-eval-print loop.  In the standard interactive
interpreter, an entirely blank logical line (i.e. one containing not even
whitespace or a comment) terminates a multi-line statement.

Indentation
-----------

Same as Python, PythoniC won't use curly brackets (``{}``).

Leading whitespace (spaces and tabs) at the beginning of a logical line is used
to compute the indentation level of the line, which in turn is used to determine
the grouping of statements. The recommend indentation for one group is 4 spaces.

Tabs are replaced (from left to right) by one to eight spaces such that the
total number of characters up to and including the replacement is a multiple of
eight (this is intended to be the same rule as used by Unix).  The total number
of spaces preceding the first non-blank character then determines the line's
indentation.  Indentation cannot be split over multiple physical lines using
backslashes; the whitespace up to the first backslash determines the
indentation.

Indentation is rejected as inconsistent if a source file mixes tabs and spaces
in a way that makes the meaning dependent on the worth of a tab in spaces; a
``Tab Error`` will be throw out. in that case.

**Cross-platform compatibility note:** because of the nature of text editors on
non-UNIX platforms, it is unwise to use a mixture of spaces and tabs for the
indentation in a single source file.  It should also be noted that different
platforms may explicitly limit the maximum indentation level.

The indentation levels of consecutive lines are used to generate INDENT and
DEDENT tokens, using a stack, as follows.

Before the first line of the file is read, a single zero is pushed on the stack;
this will never be popped off again.  The numbers pushed on the stack will
always be strictly increasing from bottom to top.  At the beginning of each
logical line, the line's indentation level is compared to the top of the stack.
If it is equal, nothing happens. If it is larger, it is pushed on the stack, and
one INDENT token is generated.  If it is smaller, it *must* be one of the
numbers occurring on the stack; all numbers on the stack that are larger are
popped off, and for each number popped off a DEDENT token is generated.  At the
end of the file, a DEDENT token is generated for each number remaining on the
stack that is larger than zero.

Here is an example of a correctly (though confusingly) indented piece of PythoniC
code:

.. code-block:: python

   def test(l) -> bool:
       if len(l) <= 1:
                     return True
       else:
         return False

Whitespace between tokens
-------------------------

Except at the beginning of a logical line or in string literals, the whitespace
characters space, tab and formfeed can be used interchangeably to separate
tokens.  Whitespace is needed between two tokens only if their concatenation
could otherwise be interpreted as a different token (e.g., ab is one token, but
a b is two tokens).
