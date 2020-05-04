---
title: 'git从入门到跑路 [5] ：tags版本标签'
author: dexfire
photos: /img/20200503135002.jpg
date: 2020-05-04 11:10:53
keywords:
description:
tags:
---

# git从入门到跑路 [5] ：tags版本标签

git-tag - Create, list, delete or verify a tag object signed with GPG

## SYNOPSIS

- 创建、修改tag
```
git tag [-a | -s | -u <keyid>] [-f] [-m <msg> | -F <file>] [-e]
	<tagname> [<commit> | <object>]
```
- 删除一个tag
`git tag -d <tagname>…​`
- tag操作
```
git tag [-n[<num>]] -l [--contains <commit>] [--no-contains <commit>]
	[--points-at <object>] [--column[=<options>] | --no-column]
	[--create-reflog] [--sort=<key>] [--format=<format>]
	[--[no-]merged [<commit>]] [<pattern>…​]
```
- 验证tag
`git tag -v [--format=<format>] <tagname>…​`

## DESCRIPTION

Add a tag reference in refs/tags/, unless -d/-l/-v is given to delete, list or verify tags.

Unless -f is given, the named tag must not yet exist.

If one of -a, -s, or -u <keyid> is passed, the command creates a tag object, and requires a tag message. Unless -m <msg> or -F <file> is given, an editor is started for the user to type in the tag message.

If -m <msg> or -F <file> is given and -a, -s, and -u <keyid> are absent, -a is implied.

Otherwise, a tag reference that points directly at the given object (i.e., a lightweight tag) is created.

A GnuPG signed tag object will be created when -s or -u <keyid> is used. When -u <keyid> is not used, the committer identity for the current user is used to find the GnuPG key for signing. The configuration variable gpg.program is used to specify custom GnuPG binary.

Tag objects (created with -a, -s, or -u) are called "annotated" tags; they contain a creation date, the tagger name and e-mail, a tagging message, and an optional GnuPG signature. Whereas a "lightweight" tag is simply a name for an object (usually a commit object).

Annotated tags are meant for release while lightweight tags are meant for private or temporary object labels. For this reason, some git commands for naming objects (like git describe) will ignore lightweight tags by default.

## OPTIONS
-a
--annotate
Make an unsigned, annotated tag object

-s
--sign
Make a GPG-signed tag, using the default e-mail address’s key.

-u <keyid>
--local-user=<keyid>
Make a GPG-signed tag, using the given key.

-f
--force
Replace an existing tag with the given name (instead of failing)

**-d
--delete
Delete existing tags with the given names.**

-v
--verify
Verify the GPG signature of the given tag names.

-n<num>
<num> specifies how many lines from the annotation, if any, are printed when using -l. Implies --list.

The default is not to print any annotation lines. If no number is given to -n, only the first line is printed. If the tag is not annotated, the commit message is displayed instead.

-l
--list
List tags. With optional <pattern>..., e.g. git tag --list 'v-*', list only the tags that match the pattern(s).

Running "git tag" without arguments also lists all tags. The pattern is a shell wildcard (i.e., matched using fnmatch(3)). Multiple patterns may be given; if any of them matches, the tag is shown.

This option is implicitly supplied if any other list-like option such as --contains is provided. See the documentation for each of those options for details.

--sort=<key>
Sort based on the key given. Prefix - to sort in descending order of the value. You may use the --sort=<key> option multiple times, in which case the last key becomes the primary key. Also supports "version:refname" or "v:refname" (tag names are treated as versions). The "version:refname" sort order can also be affected by the "versionsort.suffix" configuration variable. The keys supported are the same as those in git for-each-ref. Sort order defaults to the value configured for the tag.sort variable if it exists, or lexicographic order otherwise. See git-config(1).

--color[=<when>]
Respect any colors specified in the --format option. The <when> field must be one of always, never, or auto (if <when> is absent, behave as if always was given).

-i
--ignore-case
Sorting and filtering tags are case insensitive.

--column[=<options>]
--no-column
Display tag listing in columns. See configuration variable column.tag for option syntax.--column and --no-column without options are equivalent to always and never respectively.

This option is only applicable when listing tags without annotation lines.

--contains [<commit>]
Only list tags which contain the specified commit (HEAD if not specified). Implies --list.

--no-contains [<commit>]
Only list tags which don’t contain the specified commit (HEAD if not specified). Implies --list.

--merged [<commit>]
Only list tags whose commits are reachable from the specified commit (HEAD if not specified), incompatible with --no-merged.

--no-merged [<commit>]
Only list tags whose commits are not reachable from the specified commit (HEAD if not specified), incompatible with --merged.

--points-at <object>
Only list tags of the given object (HEAD if not specified). Implies --list.

-m <msg>
--message=<msg>
Use the given tag message (instead of prompting). If multiple -m options are given, their values are concatenated as separate paragraphs. Implies -a if none of -a, -s, or -u <keyid> is given.

-F <file>
--file=<file>
Take the tag message from the given file. Use - to read the message from the standard input. Implies -a if none of -a, -s, or -u <keyid> is given.

-e
--edit
The message taken from file with -F and command line with -m are usually used as the tag message unmodified. This option lets you further edit the message taken from these sources.

--cleanup=<mode>
This option sets how the tag message is cleaned up. The <mode> can be one of verbatim, whitespace and strip. The strip mode is default. The verbatim mode does not change message at all, whitespace removes just leading/trailing whitespace lines and strip removes both whitespace and commentary.

--create-reflog
Create a reflog for the tag. To globally enable reflogs for tags, see core.logAllRefUpdates in git-config(1). The negated form --no-create-reflog only overrides an earlier --create-reflog, but currently does not negate the setting of core.logAllRefUpdates.

--format=<format>
A string that interpolates %(fieldname) from a tag ref being shown and the object it points at. The format is the same as that of git-for-each-ref(1). When unspecified, defaults to %(refname:strip=2).

<tagname>
The name of the tag to create, delete, or describe. The new tag name must pass all checks defined by git-check-ref-format(1). Some of these checks may restrict the characters allowed in a tag name.

<commit>
<object>
The object that the new tag will refer to, usually a commit. Defaults to HEAD.