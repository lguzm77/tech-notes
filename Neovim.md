Some nice tricks -

As a replacement for `ciw` (delete an entire word and enter insert mode) just do `cw`

If you want to select some text you can use
- `viw` - selects a word only
- viW - selects all characters until the next whitespace
You can replace v with y or d to yank or delete text appropriately

## Solving Conflicts using vim figutive

To view the conflicts in a 3 view split, execute
`Gvsplitdiff!`
then use 
`:diffget` and select a buffer (2 or 3) to merge to the final file.
2 corresponds to the target branch (branch you are merging to)
3 corresponds to the merge branch (branch you are trying to merge)
