.. role:: raw-latex(raw)
   :format: latex
..

RegEx
=====

Convert document formats

Metacharacters
--------------

.. csv-table:: Metacharacters 
   :file: re-meta.csv
   :header-rows: 1


+------+---------------------------------------------------------+-----+
| C    | Description                                             | E   |
| hara |                                                         | xam |
| cter |                                                         | ple |
+======+=========================================================+=====+
| []   | A set of characters                                     | “   |
|      |                                                         | [a- |
|      |                                                         | m]” |
+------+---------------------------------------------------------+-----+
| \\   | Signals a special sequence (can also be used to escape  | ":  |
|      | special characters)                                     | raw |
|      |                                                         | -la |
|      |                                                         | tex |
|      |                                                         | :`\ |
|      |                                                         | d"` |
+------+---------------------------------------------------------+-----+
| .    | Any character (except newline character)                | “   |
|      |                                                         | he. |
|      |                                                         | .o” |
+------+---------------------------------------------------------+-----+
| ^    | Starts with                                             | “^  |
|      |                                                         | hel |
|      |                                                         | lo” |
+------+---------------------------------------------------------+-----+
| $    | Ends with                                               | “w  |
|      |                                                         | orl |
|      |                                                         | d$” |
+------+---------------------------------------------------------+-----+
| \*   | Zero or more occurrences                                | "ai |
|      |                                                         | x*" |
+------+---------------------------------------------------------+-----+
| +    | One or more occurrences                                 | “ai |
|      |                                                         | x+” |
+------+---------------------------------------------------------+-----+
| {}   | Exactly the specified number of occurrences             | “   |
|      |                                                         | al{ |
|      |                                                         | 2}” |
+------+---------------------------------------------------------+-----+
|      |                                                         | Eit |
|      |                                                         | her |
|      |                                                         | or  |
+------+---------------------------------------------------------+-----+
| ()   | Capture and group                                       |     |
+------+---------------------------------------------------------+-----+

The findall() function returns a list containing all matches.

::.. code:: python

   import re

   txt = "The rain in Spain"
   x = re.findall("ai", txt)
   print(x)
