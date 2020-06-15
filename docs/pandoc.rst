Pandoc
======

Convert document formats

Convert
-------

readme.md to readme.rst.

.. code:: python

   pandoc readme.md --from markdown --to rst -s -o readme.rst

convert multiple rst files to markdown (windows)

.. code:: python

   for %F in (*.rst) do pandoc %F --from rst --to markdown -s -o %F.md
