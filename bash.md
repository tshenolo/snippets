# Bash Cheatsheet

This cheatsheet provides common Bash commands and scripting constructs.

## Basic Commands

*   **List files and directories**:
    ```bash
    ls
    ```
    ```bash
    ls -l # Long format
    ```
    ```bash
    ls -a # Show hidden files
    ```
*   **Change directory**:
    ```bash
    cd /path/to/directory
    ```
    ```bash
    cd .. # Go to parent directory
    ```
    ```bash
    cd ~ # Go to home directory
    ```
    ```bash
    cd - # Go to previous directory
    ```
*   **Print working directory**:
    ```bash
    pwd
    ```
*   **Create a directory**:
    ```bash
    mkdir directory_name
    ```
    ```bash
    mkdir -p parent_dir/child_dir # Create parent directories if they don't exist
    ```
*   **Remove files or directories**:
    ```bash
    rm file_name
    ```
    ```bash
    rm -r directory_name # Remove directory recursively
    ```
    ```bash
    rm -f file_name # Force removal without prompting
    ```
    ```bash
    rm -rf directory_name # Force remove directory recursively (use with caution!)
    ```
*   **Copy files or directories**:
    ```bash
    cp source_file destination_file
    ```
    ```bash
    cp -r source_directory destination_directory # Copy directory recursively
    ```
*   **Move or rename files or directories**:
    ```bash
    mv old_name new_name
    ```
    ```bash
    mv source_file_or_directory destination_directory/
    ```
*   **Display file content**:
    ```bash
    cat file_name
    ```
    ```bash
    less file_name # View file content page by page (q to quit)
    ```
    ```bash
    head file_name # Display first 10 lines
    ```
    ```bash
    tail file_name # Display last 10 lines
    ```
    ```bash
    tail -f file_name # Follow file content as it grows (for logs)
    ```
*   **Print text to standard output**:
    ```bash
    echo "Hello, World!"
    ```
*   **Search for patterns in files**:
    ```bash
    grep "pattern" file_name
    ```
    ```bash
    grep -r "pattern" directory_name # Search recursively
    ```
    ```bash
    grep -i "pattern" file_name # Case-insensitive search
    ```
*   **Find files or directories**:
    ```bash
    find /path/to/search -name "filename_pattern"
    ```
    ```bash
    find . -type f -name "*.txt" # Find all .txt files in current directory and subdirectories
    ```
*   **Change file permissions**:
    ```bash
    chmod 755 file_or_directory # rwxr-xr-x
    ```
    ```bash
    chmod u+x script.sh # Add execute permission for user
    ```
*   **Change file ownership**:
    ```bash
    chown user:group file_or_directory
    ```

## Variables

*   **Declare and assign a variable** (no spaces around `=`):
    ```bash
    MY_VARIABLE="some value"
    ```
*   **Use a variable**:
    ```bash
    echo $MY_VARIABLE
    ```
    ```bash
    echo ${MY_VARIABLE} # Preferred, especially for concatenation
    ```
    ```bash
    echo "The value is: ${MY_VARIABLE}"
    ```
*   **Read-only variable**:
    ```bash
    readonly READ_ONLY_VAR="cannot change"
    ```
*   **Unset a variable**:
    ```bash
    unset MY_VARIABLE
    ```
*   **Special Variables**:
    *   `$0`: Script name
    *   `$1`, `$2`, ... `$9`: Positional parameters (arguments to script/function)
    *   `$#`: Number of positional parameters
    *   `$*`: All positional parameters as a single string
    *   `$@`: All positional parameters as separate strings
    *   `$?`: Exit status of the last command
    *   `$$`: Process ID (PID) of the current shell

## Command Substitution
*   **Store command output in a variable**:
    ```bash
    CURRENT_DATE=$(date +%Y-%m-%d)
    echo "Today is $CURRENT_DATE"
    ```
    ```bash
    # Older syntax (less common now)
    # FILES_COUNT=`ls -1 | wc -l`
    ```

## Arithmetic Expansion
*   **Perform arithmetic operations**:
    ```bash
    RESULT=$((10 + 5))
    echo $RESULT # Output: 15
    ```
    ```bash
    A=5
    B=3
    SUM=$((A + B))
    PRODUCT=$((A * B)) # Note: * needs to be escaped or quoted in some contexts if not inside $((...))
    echo "Sum: $SUM, Product: $PRODUCT"
    ```
    ```bash
    # Using expr (older)
    # C=$(expr $A + $B)
    ```

## Input/Output Redirection
*   **Redirect standard output to a file** (overwrite):
    ```bash
    ls -l > file_list.txt
    ```
*   **Redirect standard output to a file** (append):
    ```bash
    echo "New log entry" >> application.log
    ```
*   **Redirect standard error to a file**:
    ```bash
    grep "error" /var/log/syslog 2> error_log.txt
    ```
*   **Redirect standard output and standard error to a file**:
    ```bash
    ./my_script.sh > output.log 2>&1
    ```
    ```bash
    # Shorter syntax (Bash 4+)
    # ./my_script.sh &> output_and_error.log
    ```
*   **Redirect standard input from a file**:
    ```bash
    wc -l < file_list.txt
    ```
*   **Pipe output of one command to input of another**:
    ```bash
    ps aux | grep "my_process"
    ```
*   **Here Document** (pass multi-line input to a command):
    ```bash
    cat << EOF
    This is a
    multi-line
    string.
    EOF
    ```
*   **Here String** (pass single string as input, Bash specific):
    ```bash
    grep "pattern" <<< "This is a string with a pattern."
    ```

## Loops

*   **For loop** (iterating over a list):
    ```bash
    for fruit in apple banana cherry; do
        echo "I like $fruit"
    done
    ```
    ```bash
    for file in $(ls *.txt); do
        echo "Processing $file..."
    done
    ```
*   **For loop** (C-style):
    ```bash
    for (( i=1; i<=5; i++ )); do
        echo "Count: $i"
    done
    ```
*   **While loop**:
    ```bash
    counter=1
    while [ $counter -le 5 ]; do
        echo "Counter: $counter"
        ((counter++))
    done
    ```
*   **Until loop** (executes as long as condition is false):
    ```bash
    count=1
    until [ $count -gt 5 ]; do
        echo "Until count: $count"
        ((count++))
    done
    ```
*   **Loop control**:
    *   `break`: Exit the current loop.
    *   `continue`: Skip to the next iteration of the loop.

## Conditionals

*   **If statement**:
    ```bash
    read -p "Enter a number: " num
    if [ "$num" -gt 10 ]; then
        echo "Number is greater than 10."
    fi
    ```
*   **If-else statement**:
    ```bash
    if [ -f "/etc/passwd" ]; then
        echo "/etc/passwd exists."
    else
        echo "/etc/passwd does not exist."
    fi
    ```
*   **If-elif-else statement**:
    ```bash
    read -p "Enter your grade (A-F): " grade
    if [ "$grade" == "A" ]; then
        echo "Excellent!"
    elif [ "$grade" == "B" ]; then
        echo "Good!"
    elif [ "$grade" == "C" ]; then
        echo "Fair."
    else
        echo "Needs improvement or invalid grade."
    fi
    ```
*   **Test command (`[ expression ]` or `[[ expression ]]`)**:
    *   **File tests**:
        *   `-e file`: True if file exists.
        *   `-f file`: True if file is a regular file.
        *   `-d directory`: True if directory exists.
        *   `-s file`: True if file exists and has a size greater than zero.
        *   `-r file`: True if file is readable.
        *   `-w file`: True if file is writable.
        *   `-x file`: True if file is executable.
    *   **String comparisons**:
        *   `"$str1" = "$str2"` or `"$str1" == "$str2"`: True if strings are equal.
        *   `"$str1" != "$str2"`: True if strings are not equal.
        *   `-z "$str"`: True if string is empty.
        *   `-n "$str"`: True if string is not empty.
        *   `[[ "$str" =~ pattern ]]`: True if string matches regex pattern (Bash specific).
    *   **Numerical comparisons**:
        *   `num1 -eq num2`: Equal.
        *   `num1 -ne num2`: Not equal.
        *   `num1 -lt num2`: Less than.
        *   `num1 -le num2`: Less than or equal.
        *   `num1 -gt num2`: Greater than.
        *   `num1 -ge num2`: Greater than or equal.
    *   **Logical operators**:
        *   `! expression`: Logical NOT.
        *   `expression1 -a expression2`: Logical AND (within `[]`).
        *   `expression1 -o expression2`: Logical OR (within `[]`).
        *   `&&`: Logical AND (between commands or `[[]]`).
        *   `||`: Logical OR (between commands or `[[]]`).
    ```bash
    # Example with [[ ... ]] which is more flexible
    name="Jules"
    if [[ "$name" == "Jules" && -n "$name" ]]; then
        echo "Hello, Jules!"
    fi
    ```
*   **Case statement**:
    ```bash
    read -p "Enter a fruit: " fruit_name
    case "$fruit_name" in
        apple)
            echo "It's a red or green fruit."
            ;;
        banana)
            echo "It's a yellow fruit."
            ;;
        orange|tangerine) # Multiple patterns
            echo "It's an orange citrus fruit."
            ;;
        *) # Default case
            echo "Unknown fruit."
            ;;
    esac
    ```

## Functions

*   **Define a function**:
    ```bash
    # Style 1
    function greet {
        echo "Hello, $1!"
    }

    # Style 2 (more common)
    # greet() {
    #     echo "Hello, $1!"
    # }
    ```
*   **Call a function**:
    ```bash
    greet "Alice" # Output: Hello, Alice!
    ```
*   **Function arguments**:
    *   `$1`, `$2`, ...: Positional parameters passed to the function.
    *   `$#`: Number of arguments.
    *   `$*`, `$@`: All arguments.
*   **Return status**:
    *   Functions return the exit status of the last command executed by default.
    *   Use `return <numeric_code>` to specify an exit status (0 for success, non-zero for error).
    ```bash
    check_file() {
        if [ -f "$1" ]; then
            echo "File $1 exists."
            return 0 # Success
        else
            echo "File $1 does not exist."
            return 1 # Failure
        fi
    }

    if check_file "/etc/hosts"; then
        echo "Check successful."
    else
        echo "Check failed. Exit status: $?"
    fi
    ```
*   **Local variables** (scope limited to the function):
    ```bash
    my_function() {
        local my_var="I am local"
        echo $my_var
    }
    ```

## File Operations (Scripting Context)

*   **Reading a file line by line**:
    ```bash
    input_file="data.txt"
    while IFS= read -r line; do
        echo "Line: $line"
    done < "$input_file"
    # IFS= prevents leading/trailing whitespace trimming.
    # -r prevents backslash escapes from being interpreted.
    ```
*   **Checking file existence**: (see Conditionals section)
    ```bash
    if [ -f "myfile.txt" ]; then
        echo "myfile.txt exists."
    fi
    ```

## Scripting Best Practices

*   **Shebang** (specify interpreter at the beginning of the script):
    ```bash
    #!/bin/bash
    # or #!/usr/bin/env bash
    ```
*   **Comments**:
    ```bash
    # This is a single-line comment
    ```
*   **Error handling**:
    *   `set -e`: Exit immediately if a command exits with a non-zero status.
    *   `set -u`: Treat unset variables as an error when substituting.
    *   `set -o pipefail`: The return value of a pipeline is the status of the last command to exit with a non-zero status, or zero if no command exited with a non-zero status.
    ```bash
    #!/bin/bash
    set -euo pipefail
    # Your script here
    ```
*   **Exit codes**:
    *   `exit 0`: Successful execution.
    *   `exit <non-zero_number>`: Indicate an error (e.g., `exit 1`).
*   **Quoting**: Always quote variables (e.g., `"$MY_VAR"`) to prevent word splitting and globbing issues.
*   **Readability**: Use meaningful variable names, indent code, and add comments.
*   **Make script executable**:
    ```bash
    chmod +x your_script.sh
    ```
*   **Run script**:
    ```bash
    ./your_script.sh
    ```

