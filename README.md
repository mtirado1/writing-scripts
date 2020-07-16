# Writing Scripts

A collection of shell scripts for writing and processing markdown files.

All scripts print to standard output and can be used in a pipeline or with a filename as an argument.

# List of Scripts

## comments / uncomment

These scripts interpret lines that start with `@@` as a comment.

Example:

@@ This is a markdown comment!

* `comments` will print all comments in a file, removing the comment tag.
* `uncomment` will remove all the comments from a file.

`uncomment` can be used for processing a markdown file before converting it to another format.

```
uncomment document.md | pandoc > document.html
```

## yaml/rmyaml

`yaml` prints only the YAML metadata block at the beginning of a markdown file.

`rmyaml` will print the file without the header.

## makewords

Returns a list of all alphanumeric words in a file (including repetitions).

## outline

This script prints a markdown-style list with all the headers in a file. Running this script on this file prints:

```
* Writing Scripts
* List of Scripts
    * comments / uncomment
    * yaml/rmyaml
    * makewords
    * outline
    * getheader
```

## getheader

Syntax: `getheader HEADER [FILE]`

Prints the contents of the text under the first header section matched by `HEADER`, including the header.
