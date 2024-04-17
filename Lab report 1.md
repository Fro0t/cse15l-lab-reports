# cd commands

---
* no argument
```
froot@Lorins-Laptop lecture1 % cd
froot@Lorins-Laptop ~ % 
```
Absolute path: `/Users/froot/lecture1`

`cd` followed by nothing takes me to the home directory.

The output is not an error.
* directory
```
froot@Lorins-Laptop ~ % cd lecture1
froot@Lorins-Laptop lecture1 % 
```
Absolute path: `/Users/froot`

`cd` followed by a path to a directory changes the current directory to the input directory.

The output is not an error.
* file
```
froot@Lorins-Laptop lecture1 % cd Hello.java
cd: not a directory: Hello.java
```
Absolute path: `/Users/froot/lecture1`

For changing path directories, a path to a file would fail the `cd` command because a file is not a directory.

The output is an error. cd is used for changing directories. Therefore, cd followed by a path to a file would not work.


# ls commands

---
* no argument
```
froot@Lorins-Laptop lecture1 % ls
Hello.class     Hello.java      README          messages
```
Absolute path: `/Users/froot/lecture1`

`ls` followed by nothing means to list all the files and directories in the current working directory.

The output is not an error.
* directory
```
froot@Lorins-Laptop lecture1 % ls messages
en-us.txt       es-mx.txt       pl.txt          zh-cn.txt
```
Absolute path: `/Users/froot/lecture1`

`ls` followed by a directory means to list all the files and directories in the input directory.

The output is not an error.
* file
```
froot@Lorins-Laptop lecture1 % ls Hello.java
Hello.java
```
Absolute path: `/Users/froot/lecture1`

`ls` followed by a path to a file means to list the input file.

The output is not an error.


# cat commands

---
* no argument
```
froot@Lorins-Laptop lecture1 % cat
‎ 
```
Absolute path: `/Users/froot/lecture1`

`cat` followed by nothing means waiting for input. Until I input something, it will not execute anything.

The output is not an error. Technically, there isn't an output yet.
* directory
```
froot@Lorins-Laptop lecture1 % cat messages
cat: messages: Is a directory
```
Absolute path: `/Users/froot/lecture1`

`cat` followed by a directory means to display file contents for a directory, which clearly wouldn't work.

The output is an error, because cat is used for concatenating and displaying file contents.
* file

```
froot@Lorins-Laptop lecture1 % cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}%
```

Absolute path: `/Users/froot/lecture1`

`cat` followed by a file means to display file contents for that file. In this case, Hello.java was displayed just as intended.

The output is not an error.
