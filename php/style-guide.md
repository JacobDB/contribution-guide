# PHP Style Guide

Some general guidelines for how to format PHP, how to name variables, when to use variables, and more. This is specific to WordPress templates.

**NOTE:** This section is still a work in progress, and may be subject to change.

## Quotes

Wherever possible, double quotes should be used instead of single quotes. The primary reason for this is to be able to use variables within them.

```
// Good use of quotes:
$full_name = "Name: {$first_name} {$last_name}";

// Bad use of quotes:
$full_name = 'Name: ' . $first_name . ' ' . $last_name;
```

## Parenthesis

Space at the beginning and end of parenthesis should be trimmed.

```
// Good use of parenthesis:
if ($show_post = true) {
  ...
}

// Bad use of parenthesis:
if ( $show_post = true ) {
  ...
}
```

## Curly Brackets

Curly brackets should appear inline after their conditions.

```
// Good use of curly brackets
if (...) {
  ...
}

// Bad use of curly bracketse
if (...)
{
  ...
}
```

## Inline If Statements

When appropriate, inline if statements should be used. This is mostly a judgetment call, but typically when an if statement is for something simple, it should be made in to an inline statement.

```
// Good example of simple if statements
$img_alt = $img["alt"] ? " alt='$img["alt"]'" : "";

// Bad example of simple if statements
if ($img["alt"]) {
  $img_alt = " alt='$img["alt"]'";
} else {
  $img_alt = "";
}
```

## Naming Variables

Variables should use underscores to separate words. Variable names should be as generic as possible.

```
// Good example of variables
$company_name = "Weblinx, Inc.";

// Bad example of variables
$companyName = "Weblinx, Inc.";

// Bad example of variables
$weblinx = "Weblinx, Inc."
```

## Using Variables

Almost every bit of text in a theme should be made in to a variable.

```
// Good example of template content
echo "<p class='legal'>&copy; {$copyright_year} {$company_name}";

// Bad example of template content
echo "<p class='legal'>&copy; 2016 Weblinx, Inc.";
```
