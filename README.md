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

## Dependencies
- `git`
- `sed`
- `tar` and `gzip`

## Adding keywords
To add keywords to a file, create a variable that won't be removed upon compilation. For example, in C, you could use:
```c
const char *gitid = "$Git$";
```

Then, use `gitgoat -p <files(s)>`, ex. `gitgoat -p foobar.c`. This will replace the comment with something like this:
```c
const char *gitid = "$Git: 265933eba2ee713d7d6c1f293119e53c59635b13100644 d0627df69573d05d16bdf463691b85d419f10e95 0	src/bracket.c $";
```

## Stripping keywords
To strip keywords from a file, use `gitgoat -s <file(s)>`, ex. `gitgoat -s foobar.c`. This will remove the keywords and restore the keywords to simply be `$Git$`.

## Searching for keywords in a binary
To search for keywords in a binary, use `ident <file>`. This will show you the keywords in the binary.
Note that some binaries might use RCS or CVS keywords. which have the same `$` prefix. To hide non-GitGoat keywords, use `ident <file> | grep -v '$Git$'`.

## Notes
This tool is designed to do one thing and one thing well: Create & search for keywords.
A good example of how to properly use this tool is to find the commit in question, then use `git blame` to find the author.

## What's with the name?
The name was a small gag I came up with, thinking about "blaming" someone or a commit for a bug. Something like that...

