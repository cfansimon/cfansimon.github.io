---
layout: post
title:  "PHP开发sublime统一配置"
permalink: php-dev-sublime-setting
tags: [Sublime,PHP]
---

为了规范代码风格，我们团队约定sublime统一配置如下：

#### 1. 关于缩进

所用缩进都用空格；
PHP代码缩进4个空格；
HTML/CSS/JS及其衍射语言(如twig/jsx)都用2个空格;

配置如下：

打开一个PHP文件，确保sublime右下角的文件类型是PHP，然后打开配置：
Sublime Text > Preferences > Settings More > Syntax Specific - User
输入以下内容

```
{
    "tab_size": 4,
    "translate_tabs_to_spaces": true 
}
```

其他类型的文件如法炮制

#### 2. 安装CodeFormatter

打开配置：
Sublime Text > Preferences > Package Settings > CodeFormatter > Settings - User

输入一下配置，注意php的php_path，改成自己本地的

```
{
  "codeformatter_php_options": {
    "syntaxes": "php", // Syntax names which must process PHP formatter
    "php_path": "/usr/local/opt/php56/bin/php", // Path for PHP executable, e.g. "/usr/lib/php" or "C:/Program Files/PHP/php.exe". If empty, uses command "php" from system environments
    "format_on_save": true, // Format on save
    "php55_compat": false, // PHP 5.5 compatible mode
    "psr1": false, // Activate PSR1 style
    "psr1_naming": false, // Activate PSR1 style - Section 3 and 4.3 - Class and method names case
    "psr2": true, // Activate PSR2 style
    "indent_with_space": 4, // Use spaces instead of tabs for indentation
    "enable_auto_align": true, // Enable auto align of = and =>
    "visibility_order": true, // Fixes visibility order for method in classes - PSR-2 4.2
    "smart_linebreak_after_curly": true, // Convert multistatement blocks into multiline blocks
    // Enable specific transformations. Example: ["ConvertOpenTagWithEcho", "PrettyPrintDocBlocks"]
    // You can list all available transformations from command palette: CodeFormatter: Show PHP Transformations
    "passes": ["SpaceBetweenMethods", "TightConcat", "StripSpaceWithinControlStructures", "StripNewlineAfterCurlyOpen", "StripNewlineAfterClassOpen", "StripExtraCommaInArray", "SortUseNameSpace", "ReplaceBooleanAndOr", "OrderAndRemoveUseClauses", "PrettyPrintDocBlocks", "ClassToSelf", "AlignGroupDoubleArrow", "AlignEquals", "MergeElseIf"],
    // Disable specific transformations
    "exclude": []
  },
  "codeformatter_js_options": {
    "syntaxes": "javascript,json,jsx", // Syntax names which must process JS formatter
    "format_on_save": false, // Format on save
    "indent_size": 2, // indentation size
    "indent_char": " ", // Indent character
    "indent_with_tabs": false, // Indent with one tab (overrides indent_size and indent_char options)
    "eol": "\n", // EOL symbol
    "preserve_newlines": false, // whether existing line breaks should be preserved,
    "max_preserve_newlines": 10, // maximum number of line breaks to be preserved in one chunk
    "space_in_paren": false, // Add padding spaces within paren, ie. f( a, b )
    "space_in_empty_paren": false, // Add padding spaces within paren if parent empty, ie. f(  )
    "e4x": false, // Pass E4X xml literals through untouched
    "jslint_happy": false, // if true, then jslint-stricter mode is enforced. Example function () vs function()
    "brace_style": "collapse", // "collapse" | "expand" | "end-expand". put braces on the same line as control statements (default), or put braces on own line (Allman / ANSI style), or just put end braces on own line.
    "keep_array_indentation": false, // keep array indentation.
    "keep_function_indentation": false, // keep function indentation.
    "eval_code": false, // eval code
    "unescape_strings": false, // Decode printable characters encoded in xNN notation
    "wrap_line_length": 0, // Wrap lines at next opportunity after N characters
    "break_chained_methods": false, // Break chained method calls across subsequent lines
    "end_with_newline": false, // Add new line at end of file
    "comma_first": false // Add comma first
  },
  "codeformatter_css_options": {
    "syntaxes": "css,less", // Syntax names which must process CSS formatter
    "format_on_save": false, // Format on save
    "indent_size": 2, // Indentation size
    "indent_char": " ", // Indentation character
    "indent_with_tabs": false, // Indent with one tab (overrides indent_size and indent_char options)
    "selector_separator_newline": false, // Add new lines after selector separators
    "end_with_newline": false, // Add new line of end in file
    "newline_between_rules": false, // Add new line between rules
    "eol": "\n" // EOL symbol
  },
  "codeformatter_html_options": {
    "syntaxes": "html,html (twig),blade,asp,xml", // Syntax names which must process HTML formatter
    "format_on_save": false, // Format on save
    "formatter_version": "bs4", // Which formatter to use. Current options are "bs4" and "regexp". If an error occurs while loading the bs4 formatter, the regexp formatter will automatically be used
    "indent_size": 2, // indentation size
    "indent_char": " ", // Indentation character
    "indent_with_tabs": false, // Indent with one tab (overrides indent_size and indent_char options)
    "exception_on_tag_mismatch": false, // If the last closing tag is not at the same indentation level as the first opening tag, there's probably a tag mismatch in the file
    "expand_javascript": false, // (Under construction) Expand JavaScript inside of <script> tags (also affects CSS purely by coincidence)
    "expand_tags": false, // Expand tag attributes onto new lines
    "minimum_attribute_count": 2, // Minimum number of attributes needed before tag attributes are expanded to new lines
    "first_attribute_on_new_line": false, // Put all attributes on separate lines from the tag (only uses 1 indentation unit as opposed to lining all attributes up with the first)
    "reduce_empty_tags": true, // Put closing tags on same line as opening tag if there is no content between them
    "custom_singletons": "" // Custom singleton tags for various template languages outside of the HTML5 spec
  },
}
```
以上配置，PHP是保存自动格式化，其他是手动格式化。
关于手动格式化，可以配置快捷键，我自己的快捷键是 `ctrl+/`

附上配置快捷键的方法：

###### 1. 开启命令记录：
按 `ctrl+~` 启动控制台，输入 `sublime.log_commands(True)`

###### 2. 执行命令，可以在控制台取得命令的名称；
按 `command+shift+p`, 输入 `CodeFormatter: format code` 执行；
复制控制台中指令 `code_formatter`，然后关闭记录 `sublime.log_commands(False)`;

###### 3. 配置快捷键
打开配置 Sublime Text > Preferences > key Bindings - User
新增一条

```
{ "keys": ["ctrl+forward_slash"], "command": "code_formatter"},
```


