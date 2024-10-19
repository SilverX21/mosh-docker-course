# The Linux Command Line

Let's go to Docker Hub and get the Ubuntu image:
https://hub.docker.com/_/ubuntu

## 1- Docker pull and Docker run

Instead of using the `docker pull ubuntu` command, you can use a shortcut: `docker run ubuntu`.
If docker doesn't find the image you specified in the command, it will first pull the image and then run it.

You will see that the container will stop running after it's pulled. To confirm this you can use the command `docker ps` that will give you the list of running processes.
If we run `docker ps -a` it will list all the processes, even those that are not running.

## 2 - Running commands in ubuntu

We can run the command `docker run -it ubuntu`, this will run the container in the interactive mode.

![docker shell mode](images/1-docker-shell.png)

this will result in a shell. This will pick up our command and pass it to the operating system for execution.

If we run the command `echo $0` it will show us the location of the shell programm.

## 3 - apt package manager

`apt` is a package manager for linux (ubuntu in this case). It works similar to the `winget` from Windows.

In this case, we will install the package nano, that's a basic text editor for linux. So, to install it, we will run the following: `apt install nano`

![apt install error](images/2-apt-install-error.png)

After running this command, it will result on a error because the apt command cannot find a reference to the nano package, because it might not be installed, we can check that using the `apt list` command.
To solve this, we need to update the apt database using the command `apt update`.
So, before we isntall a package, we must first update the list/database of packages and then install the needed package.
To remove this package, you just need to run `apt remove nano`.

## 4- Most used commands that we are going to use

- `pwd` - prints the current working directory
- `ls` - prints the directory files
- `ls -l` - prints the directory files in an more detailed way
- `ls -a` - shows all the files and directories (including the ones that are hidden)
- `mv old_folder_name new_folder_name` - changes the folder name to a new name
- `touch file_name.file_extension` - creates a file with a given name and extension. We can also create many files in one go, like this `touch file1.txt file2.txt` -`rm file_name` - removes a given file. We can also delete many files like this `rm file1.txt file2.txt` or we can use a rule, something like this `rm file*` (we are saying remove every file that starts with the name "file")
- `rm -r directory_name` - removes a given directory. if we try without the `-r` it will fail. So use that flag to remove a directory
- `cat file_name` - checks the content of a given file
- `cat file_name1 file_name2 ...` - we can combine multiple files together and check the output like this `cat file1.txt file2.txt`and it will the output of the files specified
- `more file_name` - is adjusted to check longer files. To navigate between the pages, you just need to click in the "space bar". If you want to check a line at a time, you can press "Enter". To exit press the "Q" key
- `>` this is the redirect operator. This redirects an output to something or somewhere else. In this case, we can do something like this: `cat file_name1 > file_name2`. This will pick the content of the `file_name1` and write it in the `file_name2`. We can combine multiple files and merge them into one like this - `cat file1.txt file2.txt > combine.txt`
- `grep word_to_find file_name` - searches for a given word in a file. This is case sensitive
- `grep -i word_to_find file_name` - the same as the above, but it's not case sensitive
- `grep word_to_find file_name1 file_name2 ...` - searches in the provided files the given word. We can also use a pattern, like this `grep hello file*`
- `grep -i -r word_to_find directory_name` - searches recursively (`-r`) in a given directory, and it's sub directories, for the following word. Example: `grep -i -r hello .` (`.` is for the current directory). we can combine `-i -r` in a single command like this `grep -ir hello .`

- `find` this command will return all the files inside a directory recursively.
- `find directory_path` will show all the files and directories (recursively) inside a given directory that is passed
- `find -type d` - shows only the directories
- `find -type f` - shows only the files
- `find -type f -name "file_name"` - shows only the files that start with a given name. We can also use a pattern like this: `find -type f -name "f*"`. We can also use case insensitive matching like this: `find -type f -iname "f*"`

Example: if we want to find all files that are python files inside this lixus directory, we can do this like this: `find -type f -iname "*.py"`. If we want to store it inside a file, we can do something like this: `find -type f -iname "*.py" > python_files.txt`

- `;` - we can use the `;` so chain multiple commands in one go. Example: `mkdir test ; cd test ; echo done` -> this will execute all of the commands in one go
- `&&` - we can use the and operator to chain multiple commands as well. The main difference is that this command will stop if one of the commands doesn't work. Example `mkdir test && cd test` if the first command doesn't work, the execution will be stopped, and no other command will be executed. If we use `;` all the commands will be executed regardless of success or failure.
- `||` - this is the or operator. It works just like the `&&` and `;` operators, but it works like this:
  if we have something like `mkdir test || echo "directory exists"` if the first command doesn't work, it will execute the second command, else it will execute the first command only.
  `|` - this is the pipe operator. This works like this: `ls /bin | less` -> first it will execute the first command and then will provide the output of the first command as as input to the second command.
- `\` - we can use the backslash operator to have split the commands into multiple lines. When we use the `\` we will press Enter and then continue to the other commands. Example:
  `mkdir test;\`
  `cd test;\`
  `echo done`

## Environment variables

`printenv` - prints the environment variables in the machine
`printenv variable_name` - prints a given environment variable. We can also use the echo, but we need to prepend a $ to the variable name, like this: `echo $PATH`
`export variable_name` - sets/creates a new environment variable and it's sabed in the current session. If we close the terminal and try to print it again, it won't work, because it's session-dependent
`>>` - works as the `>` operator, but this, instead of replacing the content, will append it to the end of the file. Example: `echo Hello >> test1.txt`
`source file_name` - this command will reload a given file in the session
