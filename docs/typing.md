convert multiple rst files to markdown (windows)
```
for %F in (*.rst) do pandoc %F --from rst --to markdown -s -o %F.md
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxOTgyMDgxOF19
-->