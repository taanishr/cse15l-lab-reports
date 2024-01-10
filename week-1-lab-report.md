# CD:

**1. No arguments**

Output:
```
[user@sahara ~]$ cd
[user@sahara ~]$
```

a) Current working directory when command was run:
```/home```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cd is ran with no arguments, the directory is changed to the home directory ```/home```.

c) CD doesn't print anything to the terminal when successful, so no output means it worked.

**2. Path to a directory as an argument**

Output:

```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$
```

a) Current working directory when command was run:
```/home```

b) The filesystem consisted of a home directory, which contained a lecture1 subfolder (containing a messages directory with some files), a java binary, a java file, and a readme. When cd is ran with a directory as an argument (```lecture1/```), the directory is changed to the directory ```/home/lecture1```

c) CD doesn't print anything to the terminal when successful, so no output means it worked.

**3. Path to a file as an argument**

Output:

```
[user@sahara ~/lecture1]$ cd Hello.java 
bash: cd: Hello.java: Not a directory
```

a) Current working directory when command was run:
```/home/lecture1```

b) When cd is ran with a file as an argument (Hello.java), an error statement is printed to the terminal: ```bash: cd: Hello.java: Not a directory```. Files aren't directories, so cd cannot change your current working directory to one.

c) The output is an error because files aren't directories, so CD cannot change change your current working directory to one.
