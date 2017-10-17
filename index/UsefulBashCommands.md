[Back to Guides](../README.md)
# Useful Bash Commands

>Important: All the following commands are case sensitive! Assume all commands should be entered as lower case unless otherwise specified.

>Important: The "man" command allows you to bring up the manual page of a given command. To see further options and more detailed information about commands enter "man" followed by the command. EX: $ man mkdir

### ls
  - Lists information about the files in the current directory
  ``` shell
  $ ls
  ```
  
### mkdir
  - Creates a directory of the specified name
  ```shell
  $ mkdir aNewDirectory
  ```

### rmdir
  - Removes a directory of a given name
  ```shell
  $ rmdir aNewDirectory
  ```
 
### cd
  - Change directory. Will change to home directory if no directory name is provided. Otherwise changes to specified directory.
  ```shell
  $ cd
  ```
  
  ```shell
  $ cd aNewDirectory
  ```
  
### touch
  - Creates a blank file with a specified name
  ```shell
  $ touch aNewFile.txt
  ```

### rm
  - Removes a specified file. WARNING: This is permanent. There is no recycle bin.
  ```shell
   $ rm aNewFile.txt
  ```
 
### cat
  - Display the contents of a file
  ```shell
  $ cat aNewFile.txt
  ```
  
### pwd
  - Displays the name of the current directory
  ```
  $ pwd
  ```
  
### head
  - Displays the first 10 lines of a file
  ```shell
  $ head aNewFile.txt
  ```
  
### tail
  - Displays the last 10 lines of a file
  ```shell
  $ tail aNewFile.txt
  ```
  
### cp
  - Copy specified file to a new specified file
  ```shell
  $ cp aNewFile.Txt anotherNewFile.txt
  ```
  
### mv
  - Rename a specified file or directory
