
## Your Goals

### 1. Get the boilerplate running

- Follow the instructions in the **Getting Started** section to get the boilerplate code, and get it running on your local systems.


### 2. Understand the **Usage** and **Specifications** sections

- The **usage** section details the end-user interface. Understand how the CLI tool will be used by a user who gets your software.

- The **specification** section details how you should actually implement each functionality, what happens in the background. This is your logic.

### 3. Familiarize yourself with the source code in `task.c`

- Take a look at all the helper functions, interfaces, and structures in the source file. *Simply try to understand what each function does: its input and output.* 

> Start from the `main()` function, and trace your way through the function calls.

### 4. Start implementing one use-case at a time

- Start with the first use-case in the **usage** section.

- Find the relevant portion of the code (start looking from `main()`!) and write your code to make appropriate function calls and/or operations to implement it.

- **Compile and Run** frequently, to ensure that you are headed in the right direction.

- Got one case running? Great! - Let us know.

(**implement-execute-test** and repeat for the rest of the use-cases).

### **[Bonus]** 5. Add a Task *Completion Date*

- Include an additional `date_of_completion` field that records _when_ the task is marked as done.

> The functions to get the current date and time, in the required character-array format, are already provided as helpers!
> Note, however, that you'll need to modify the task structure to make this happen.

### **[Bonus]** 6. Run the Automated Tests

- Follow the instructions in the **Run Automated Tests** section to run automated tests, that wil evaluate multiple edge-cases of your application.

- Again, **implement-execute-test** and repeat for each use case.


## Todo CLI Usage

### 1. Help

Executing the command without any arguments, or with a single argument help prints the CLI usage.

```
$ ./task help
Usage :-
$ ./task add 2 hello world    # Add a new item with priority 2 and text "hello world" to the list
$ ./task ls                   # Show incomplete priority list items sorted by priority in ascending order
$ ./task del INDEX            # Delete the incomplete item with the given index
$ ./task done INDEX           # Mark the incomplete item with the given index as complete
$ ./task help                 # Show usage
$ ./task report               # Statistics
```

### 2. List all pending items

Use the ls command to see all the items that are not yet complete, in ascending order of priority.

Every item should be printed on a new line. with the following format

```
[index] [task] [priority]
```

Example:

```
$ ./task ls
1. change light bulb [2]
2. water the plants [5]
```

index starts from 1, this is used to identify a particular task to complete or delete it.

### 3. Add a new item

Use the add command. The text of the task should be enclosed within double quotes (otherwise only the first word is considered as the item text, and the remaining words are treated as different arguments).

```
$ ./task add 5 "the thing i need to do"
Added task: "the thing i need to do" with priority 5
```

### 4. Delete an item

Use the del command to remove an item by its index.

```
$ ./task del 3
Deleted item with index 3
```

Attempting to delete a non-existent item should display an error message.

```
$ ./task del 5
Error: item with index 5 does not exist. Nothing deleted.
```

### 5. Mark a task as completed

Use the done command to mark an item as completed by its index.

```
$ ./task done 1
Marked item as done.
```

Attempting to mark a non-existed item as completed will display an error message.

```
$ ./task done 5
Error: no incomplete item with index 5 exists.
```

### 6. Generate a report

Show the number of complete and incomplete items in the list. and the complete and incomplete items grouped together.

```
$ ./task report
Pending : 2
1. this is a pending task [1]
2. this is a pending task with priority [4]

Completed : 3
1. completed task
2. another completed task
3. yet another completed task
```

## Todo CLI Specification

1. The app can be run in the console with `./task`.

2. The app should read from and write to a `task.txt` text file. Each task occupies a single line in this file. Each task should have an associated priority, an integer.

> Priority denotes how important a task is, if it is a high priority task, it should be completed earlier. Priority is denoted using an integer. The lower the number, the higher the priority.
   
Here is an example of a list of 2 tasks in the file.
   ```
   1 Buy milk
   2 Complete the project
   ```

3. A completed task is written to a `done.txt` text file. Each task should enapsulate all fields of the original task.

4. Priority can be any integer _greater than_ or _equal to_ 0. 0 being the highest priority

5. If two task have the same priority, the task that was added first should be displayed first.

   The application must open the files task.txt and done.txt from where the app is run, and not where the app is located. 

   ```
   $ cd /path/to/plans

   $ /path/to/apps/task ls
   ```

   The application should look for the task files in `/path/to/plans`, since that is the user’s current directory.

6. The files should always be sorted in order of the priority, i.e., the task with the highest priority should be first item in the file.
   
> Please note that the programming task can and preferably, should be completed without the use of any additional packages.



## [Optional] Run Automated Tests

>If you are able to set up npm by following the steps below, great! You can validate that your app works as expected.

>Otherwise, we'll do this for you, when we are evaluating the project. In addition to the test cases mentioned here, we'll add on a few more during the evaluation.

### 1. Install Node.js

You need to have `npm` installed in your computer for the following steps. It comes with Node.js and you can get it by installing Node from https://nodejs.org/en/

### 2. Install dependencies

Run `npm install` to install all dependencies.

### 3. Create a symbolic link to the executable file

#### On Windows

To create a symbolic link on Windows, you'll need to run either the Windows Command Prompt, or Windows Powershell **with administrator privileges**. To do so, right-click on the icon for Command Prompt, or Powershell, and choose the _"Run as Administrator"_ option.

**Command Prompt:**

```
> mklink task task.bat
```

**Powershell:**

```
> cmd /c mklink task task.bat
```

#### On \*nix:

Run the following command in your terminal:

```
$ ln -s task.sh task
```

### 4. Try running tests.

Now run `npm test` and you will see all the tests failing. As you fill in each functionality, you can re-run the tests to see them passing one by one.
