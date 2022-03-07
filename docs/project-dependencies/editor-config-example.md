An [EditorConfig](https://editorconfig.org/) file in combination with a [IDE specific plugin](https://editorconfig.org/#download) helps maintain consistent coding styles for multiple developers working on the same project across various editors and IDEs. You define coding styles for any file format and mainly define things like indent size and style.  Sounds like such a little thing but how annoying is it when you've coding js with `2 spaces`, someone else contributes to your codebase, and the next time you open that file everything is `4 spaces`, or worse `indent 2`.

This config lives in the root of your project and is named `.editorconfig`:

```
root = true

[*]
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[**.{rb,pp}]
indent_style = space
indent_size = 2
continuation_indent_size = 2
quote_type = double

[**.{yml,yaml}]
indent_style = space
indent_size = 2

[**.{txt}]
indent_style = space
indent_size = 2

[**.{js}]
indent_style = space
indent_size = 2

[**.{jsx}]
indent_style = space
indent_size = 2

[**.{scss}]
indent_style = space
indent_size = 2
```