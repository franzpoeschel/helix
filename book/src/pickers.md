## Using pickers

Helix has a variety of pickers, which are interactive windows used to select various kinds of items. These include a file picker, global search picker, and more. Most pickers are accessed via keybindings in [space mode](./keymap.md#space-mode). Pickers have their own [keymap](./keymap.md#picker) for navigation.

### Filtering Picker Results

Most pickers perform fuzzy matching using [fzf syntax](https://github.com/junegunn/fzf?tab=readme-ov-file#search-syntax). Two exceptions are the global search picker, which uses regex, and the workspace symbol picker, which passes search terms to the language server. Note that OR operations (`|`) are not currently supported.

If a picker shows multiple columns, you may apply the filter to a specific column by prefixing the column name with `%`. Column names can be shortened to any prefix, so `%p`, `%pa` or `%pat` all mean the same as `%path`. For example, a query of `helix %p .toml !lang` in the global search picker searches for the term "helix" within files with paths ending in ".toml" but not including "lang".

You can insert the contents of a [register](./registers.md) using `Ctrl-r` followed by a register name. For example, one could insert the currently selected text using `Ctrl-r`-`.`, or the directory of the current file using `Ctrl-r`-`%` followed by `Ctrl-w` to remove the last path section. The global search picker will use the contents of the [search register](./registers.md#default-registers) if you press `Enter` without typing a filter. For example, pressing `*`-`Space-/`-`Enter` will start a global search for the currently selected text.

### Reusing existing views

Pressing `Alt-r` opens the selected item like `Enter`, but never in the current
view. If the target file is already displayed in another view, that view is focused.
If it is displayed in multiple other views, the most recently focused one is chosen.
If it is not displayed in another view, a new split is created. With a single view,
the split follows the view's longer axis; with multiple views, it follows the current
view's layout axis.

The key can be changed with the `picker-open-existing` option in the `[editor]`
section. `Alt-Enter` keeps its previous behavior of opening the selected item in
the background without closing the picker.
