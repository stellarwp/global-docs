# Editorconfig

`.editorconfig` ensures consistent coding styles and settings across different editors and IDEs.

These are settings like indentation and character encoding. Normalizing them makes collaboration smoother and code more uniform.

## How to Use

- Copy the contents of the code below.
- Create an `.editorconfig` file at the root of your project.
- Paste the contents into the file.

These steps will automatically configure your text editor or IDE settings according to the defined rules when you open the project.

In some cases, you may have to install a plugin for your editor to enable this feature, or quit and restart your editor for it to take effect.

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
indent_size = 4
tab_width = 4
indent_style = space
insert_final_newline = true
trim_trailing_whitespace = true

[*.txt]
trim_trailing_whitespace = false
```
