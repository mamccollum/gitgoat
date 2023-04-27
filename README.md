# 🐐 GitGoat: RCS-like identification keywords for Git!

GitGoat is a tool for adding RCS-like identification keywords to files in Git repositories.

## Why?
When I used RCS for a short while, I found one specific feature VERY helpful: `ident`. It's a command that searches for RCS keywords in a file and displays the keyword and only the keyword. 

This is useful for tracking where bugs come from in projects that compile to binaries; you would be able to use `ident` and it would show the file name, the version, date, and author of the latest change to the file.

Here's an example from NetBSD:
```
$ ident /bin/cat
/bin/cat:
     $NetBSD: crt0.S,v 1.4 2018/11/26 17:37:45 joerg Exp $
     $NetBSD: crt0-common.c,v 1.23 2018/12/28 20:12:35 christos Exp $
     $NetBSD: crti.S,v 1.1 2010/08/07 18:01:33 joerg Exp $
     $NetBSD: crtbegin.S,v 1.1 2010/08/07 18:01:33 joerg Exp $
     $NetBSD: cat.c,v 1.57 2016/06/16 00:52:37 sevan Exp $
     $NetBSD: crtend.S,v 1.1 2010/08/07 18:01:33 joerg Exp $
     $NetBSD: crtn.S,v 1.1 2010/08/07 18:01:34 joerg Exp $
```

# Usage
See `man gitgoat` for detailed usage information.

## Adding keywords
To add keywords to a file, create a variable that won't be removed upon compilation. For example, in C, you could use:
```c
const char *gitid = "%ID%";
```

Then, use `gitgoat prep <files(s)>`, ex. `gitgoat prep foobar.c`. This will replace the comment with something like this:
```c
const char *gitid = "%ID foobar.c cc16f9aad12cf01e5865b557eeef643e23807ee2%";
```

## Notes
This tool is designed to do one thing and one thing well: Create & search for keywords.
A good example of how to properly use this tool is to find the commit in question, then use `git blame` to find the author.

## What's with the name?
The name was a small gag I came up with, thinking about "blaming" someone or a commit for a bug. Something like that...

