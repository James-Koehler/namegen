# namegen



A simple (and very over-engineered) commandline tool to quickly generate project names, which I am now rewriting in Rust as an effort to learn it.

The file in /data/ is a template (and the default behavior) for adding in your own prefixes and suffixes.

# Arguments

## Generating a Name

| Argument | Description |
| :------- | :---------- |
| No Argument | Generates a name with with 1 prefix and 1 suffix, which are randomly selected from a random category. |
| -l, --length | Sets the amount of prefixes to use. This must be an integer. Not specifying the prefixes using --prefix (-p) will result in random prefixes. Must be greater than 1. |
| -p, --prefix | Sets the prefix type, and must be one of the valid prefix types. If --length (-l) is used, it will expect the same amount of arguments as prefixes requested by --length (-l). |
| -s, --suffix | Sets the suffix type, and must be one of the valid suffix types. This can only be used once. |

## Configuration Arguments

**Note: These control how the output is generated for future use, and a name cannot be generated while any of these are in use.**

| Argument | Description |
| :------- | :---------- |
| -pl, --prefix-list | Outputs all valid prefix categories. It can be entered alone, or with one of the valid prefix categories, at which point it will output the prefixes of that category. |
| -sl, --suffix-list | Outputs all valid suffix categories. It can be entered alone, or with one of the valid suffix categories, at which point it will output the suffixes of that category. |
| -r, --reset | Resets the prefix and suffix lists used by the command to their default state. |
| -dp, --delete-prefix | Deletes the specified prefix from the valid prefixes. |
| -ds, --delete-suffix | Deletes the specified suffix from the valid suffixes. |
| -h, --help | Displays this information. |
| -v, --version | Displays the version number. |

# Usage

Usage is simple! namegen can be run with or without arguments, making the names it generates infinitely unique, as long as the provided prefix and suffix lists have enough variety.

## Usage Rules

Some arguments cannot be used with others in order to prevent unwanted behavior. Arguments used for generating names cannot be used with other commands. Some of the other commands are incompatible with eachother as well. For example:

`namegen -l 2` is a valid command.

`namegen -l 2 -r` is not a valid command.

| Argument | Compatible arguments |
| :--- | :--- |
| -l, --length | -p, --prefix, -s, --suffix |
| -p, --prefix | -l, --length, -s, --suffix |
| -s, --suffix, | -l, --legnth, -p, --prefix |
| -pl, --prefix-list | None |
| -sl, --suffix-length | None |
| -r, --reset | None |
| -dp, --delete-prefix | None |
| -ds, --delete-suffix | None |
| -h, --help | All arguments |
| -v, --version | None |

## Example Outputs

| Input | Output |
| :---  |  :--- |
| namegen | Big Gravy |
| namegen -l 2 | Big Titanium Gravy |
| namegen -l 2 -p colors metals | Blue Steel Gravy |
| namegen -s animals | Big Shark |
| namegen -pl | colors, metals, sizes |
| namegen -pl colors | Blue, Red, Purple, Green, Silver, Black, White |


# Using Your Own Prefixes/Suffixes

As these are stored in plaintext, the method for adding, removing, or modify individual prefix/suffix types is simple!

## File Structure

```
./data/
    prefix/
        colors
        metals
        etc...
    suffix/
        foods
        animals
        etc...
```

This file structure is automatically generated the first time the command is run, or if it fails to detect the files. Adding your own set of prefixes or suffixes is as simple as dropping in a file with the name of the set where the contents of the file are the words of that set.

## File Rules

### Naming

File names **must** be one word! Adding spaces to the file name will make it inaccessible. The only non-alphanumeric character allowed in a file name is underscore. The file should also have no extension, despite the fact that it stores plaintext.

Some valid examples:
`myCoolWords`, `my_cool_words`

Some invalid examples:
`my cool words`, `my-cool-words` `my_cool_words.txt`, `my_cool_words.words`, `my_cool_words.mycoolfileextenstion`

To protect from unexpected behavior like crashes or arguments being processed incorrectly, lists with invalid names won't be loaded. If your set of words really needs a name with spaces, you can snake_case or camelCase them.

### Contents

Contents should be stores as one word per line. You can add spaces here if you want, but words are separated by new lines.

A valid example:
```
my
cool
words
look at this!
```

An example that may not format correcly:
```
my,cool,words,look at this!
```

## Prefix/Suffix Set Example

Let's say you want to make a set of prefixes called `my_cool_words`. You want this to contain a list, broken up by new lines, of the words you would like to fall within that category. The contents may look something like this:

```
my
cool
words
```

Now that you have generated your file, it just needs to be installed into the file structure. As this is a prefix list we would store it ay `.data/prefix/my_cool_words`. If this was a suffix though it would fall into `./data/suffix/my_cool_words`.

And you're done! Adding your own words is simple, and modifying existing words is just as simple as editing one of the files already there.

# Roadmap

## Cool Features

- [ ] Automatically making sets of prefixes/suffixes from the command line via arguments
- [ ] Output in cool formatted ASCII art
- [ ] Customized output for piping through to project generation tools
- [ ] Expand available default words (Always ongoing)

## Issues

- None! (Let's hope it stays that way.)

# Credits

Written by James Koehler.

For bug reports, questions, or suggestions, please reach out at jameskoehler@protonmail.com or add an issue on the github.
