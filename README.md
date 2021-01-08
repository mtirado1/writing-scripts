# Writing Scripts

A collection of shell scripts for writing and processing markdown files.

All scripts print to standard output and can be used in a pipeline or with multiple filenames as arguments

# List of Scripts

## comments / uncomment

These scripts interpret lines that start with `@@` as a comment.

Example:

@@ This is a markdown comment!

* `comments` will print all comments in a file, removing the comment tag. An additional flag (-l or --lines) will print the line number where the comment is located, along with the comment.
* `uncomment` will remove all the comments from a file.

`uncomment` can be used for processing a markdown file before converting it to another format.

```
comments --lines document.md > comments.txt
uncomment document.md | pandoc > document.html
```

## yaml / rmyaml

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
    * yaml / rmyaml
    * makewords
    * outline
    * getheader
* Some examples
    * Word count
    * Creating an index
    * TODO comments
    * Simple YAML parsing
```

## getheader

Syntax: `getheader HEADER [FILES]`

Prints the contents of the text under the first header section matched by `HEADER`, including the header and other sub-headers.

# Some examples

## Word count

By using `makewords` before `wc`, special symbols are removed (such as header tags and quotes common in markdown files).

```
makewords ch01.txt ch02.txt ch03.txt | wc -l
```

Unique words can also be calculated using `sort` and `uniq`:

```
makewords ch01.txt ch02.txt ch03.txt | sort | uniq | wc -l
```

## Creating an index

Since all commands can work with multiple files, it's possible to generate a header index

```
outline ch01.md ch02.md ch03.md > index.md
```

## TODO comments

Comments can be used to store marks, comments, or notes in a markdown file.

```sh
#!/bin/sh

for  file in documents/*.md; do
	echo "  To-do for $file:"
	comments -l "$file" | grep TODO
done
```

## Simple YAML parsing

Basic metadata can be obtained using grep and sed.

```
yaml header.md | grep ^title | sed 's/^.*:\s*//'
```
