# cd

**1. No arguments**

Output:
```
[user@sahara ~]$ cd
[user@sahara ~]$
```

a) Current working directory when command was run:

```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cd is ran with no arguments, the directory is changed to the home directory `/home`.

c) CD doesn't print anything to the terminal when successful, so no output means it worked.

**2. Path to a directory as an argument**

Output:

```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$
```

a) Current working directory when command was run:

```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cd is ran with a directory as an argument (`lecture1/`), the directory is changed to the directory `/home/lecture1`

c) CD doesn't print anything to the terminal when successful, so no output means it worked.

**3. Path to a file as an argument**

Output:

```
[user@sahara ~/lecture1]$ cd Hello.java 
bash: cd: Hello.java: Not a directory
```

a) Current working directory when command was run:

```
/home/lecture1
```

b) When cd is ran with a file as an argument (Hello.java), an error statement is printed to the terminal: `bash: cd: Hello.java: Not a directory`. Files aren't directories, so cd cannot change your current working directory to one.

c) The output is an error because files aren't directories, so CD cannot change change your current working directory to one.

# ls

**1. No arguments**

Output:

```
[user@sahara ~]$ ls
lecture1
```

a) Current working directory when command was run:

```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When ls is ran with no arguments, it prints the directories and files (in this case, lecture1) inside the current working directory (`/home`)

c) The output was not an error

**2. Path to a directory as an argument**

Output:

```
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
```

a) Current working directory when command was run:
`/home`

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When ls is ran with a directory as an argument (`lecture1/`), it prints the directories and files inside the directory given as an argument.

c) The output was not an error

**3. Path to a file as an argument**

Output:

```
[user@sahara ~/lecture1]$ ls messages/es-mx.txt 
messages/es-mx.txt
```

a) Current working directory when command was run:

```
/home/lecture1
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When ls is ran with a file as an argument (`messages/es-mx.txt`), it prints the path to the file from the current working directory (which may NOT be the home directory) to the terminal (`messages/es-mx.txt`)

c) The output was not an error

# cat

**1. No arguments**

Output:

```
[user@sahara ~]$ cat

```

a) Current working directory when command was run:

```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cat is ran with no arguments, the terminal enters a mode where anything typed will be printed to the terminal. To escape this, the user must press CRTL+C.

c) The output was not an error

**2. Path to a directory as an argument**

Output:

```
[user@sahara ~]$ cat lecture1/
cat: lecture1/: Is a directory
```

a) Current working directory when command was run:

```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cat is ran with a directory as an argument (`lecture1/`), it prints an error statement because cat reads the text contents of files, and directories have no text contents.

c) The output was an error because cat reads the text contents of files, and directories have no text contents.

**3. Path to a file as an argument**

Output:

```
[user@sahara ~]$ cat lecture1/messages/en-us.txt 
Hello World!
```

a) Current working directory when command was run:
```
/home
```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cat is ran with a file path as an argument (`lecture1/messages/en-us.txt`), it prints the text contents of the file. When cat is run with multiple arguments (each denoting a file path), it prints the text contents of each file one after another.

c) The output was not an error.
