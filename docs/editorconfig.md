# EditorConfig

`.editorconfig` helps maintain consistent coding styles and settings across different editors and IDEs. This includes things like indentation and character encoding.

Using it helps with smoother collaboration and more uniform code.

## How to Use

- Copy the code below.
- Create an `.editorconfig` file in your project's root.
- Paste the copied code into this file.

This will set your text editor or IDE to follow these rules automatically when you open the project.

**Note:** You might need to install a plugin for your editor, or restart it for the changes to take effect.

## `.editorconfig` File

```ini
# StellarWP EditorConfig
#
# https://github.com/stellarwp/global-docs/blob/main/docs/editorconfig.md
# https://editorconfig.org

root = true

[*]
charset = utf-8
end_of_line = lf
indent_style = tab
insert_final_newline = true
tab_width = 4
trim_trailing_whitespace = true

[**.{jshintrc,json,scss-lint,yml}]
indent_style = space
indent_size = 4

[*.txt]
trim_trailing_whitespace = false
```
