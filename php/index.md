# PHP

[Style Guide](style-guide.md) | [Resources](resources.md)

In this section, you'll learn how to format PHP and name variables.

## Quick Notes

- Use double quotes wherever possible.
- Use `"Some {$example} text"` instead of `"Some " . $example . " text"`
- Trim extra spaces at the beginning and end of parenthesis. i.e. `($example = true)`, not `( $example = true )`
- Curly brackets go on the same line as the opening statement, with one preceeding space. i.e. `if ($example = true) {`
- When appropriate, inline if statemnts should be used. i.e. `$img_alt = $img["alt"] ? " alt='$img["$alt"]'" : "";`
- Use underscores to separate words in variables. i.e. `$example_variable`, not `$exampleVariable`
- Name variables in a general way when appropriate. i.e. `$company_name`, not `$weblinx`
- Nearly all text in a template should be set up as variables. i.e. `$company_name = "Weblinx"; echo $company_name;`, not `echo "Weblinx";`
