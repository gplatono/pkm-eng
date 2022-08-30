# List of useful shell commands

## Navigation

* **cd \[OPTIONS\] \[PATH\]**: "change directory" - changes the working directory to the one specified by PATH.
  ```
  Example: cd ~/
  Result: Goes to the home directory.
  ```
  Executing *cd \[PATH\]* is equivalent to executing *popd && pushd \[PATH\]*.

* **pwd \[OPTIONS\]**:  "print working directory" - prints the current working directory.
  ```
  Example: pwd
  Result: Prints the current directory, e.g., /home/USERNANE/
  ```

* **dirs \[OPTIONS\]**: prints the current directory stack. The top of the stack always points to the current working directory. Useful options are 
  * -v: print the stack as numbered list.
  * -l: print long paths.
  ```
  Example: dirs -v
  Result: prints
  
  0: WORKING_DIRECTORY
  1: PATH1
  ...
  N: PATHN
  ```
* **pushd \[OPTIONS\] \[PATH\]**: "push directory" - pushes the directory specified by PATH onto the top of the directory stack and navigates to that directory.
  ```
  Example: let the current stack be
  0: WORKING_DIRECTORY
  1: PATH1
  2: PATH2

  then running *pushd NEW_WORKING_DIRECTORY* will result in

  0: NEW_WORKING_DIRECTORY
  1: WORKING_DIRECTORY
  2: PATH1
  3: PATH2
  ```

  Special arguments +N, -N allow to navigate to the Nth directory in the directory stack. +N counts from the top, -N counts from the bottom of the stack. *pushd* navigates to selected dierectory and the stack is rotated, i.e., the bottom of the stack goes on the previous top.

  ```
  Example: let the current directory stack be
  0: PATH 0
  1: PATH 1
  ...
  N: PATN N
  N+1: PATH N+1
  ...
  M: PATH M

  Executing *pushd +N* leads to the following new stack:

  0: PATH N
  1: PATH N+1
  ...
  M-N: PATH M
  M-N+1: PATH 0
  ...
  M: PATH N-1
  ```

* **popd \[OPTIONS\]**: "pop directory" - pops the current working directory from the directory stack and makes the next entry the new working directory.
  ```
  Example: let the current stack be:
  0: PATH 0
  1: PATH 1
  ...
  N: PATN N

  Then *popd* changes it to
  
  0: PATH 1
  1: PATH 2
  ...
  N-1: PATN N
  ```
## Lookup and inspecting

* **ls \[OPTIONS\]"": "list directory contents" - lists the contents of the current working directory.
  
#linux, #shell