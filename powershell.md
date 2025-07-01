# PowerShell Cheatsheet

This cheatsheet covers common PowerShell cmdlets and scripting features.

## Core Concepts

*   **Cmdlets (Verb-Noun)**: Small, single-function commands (e.g., `Get-Process`, `Set-Location`).
*   **Objects**: PowerShell works with objects, not just text. Output from one cmdlet can be piped to another.
*   **Pipeline (`|`)**: Sends the output (objects) of one cmdlet to the input of another.
*   **Help System**:
    ```powershell
    Get-Help Get-Process # Help for a specific cmdlet
    Get-Help Get-Process -Examples
    Get-Help Get-Process -Full
    Get-Help about_Variables # Conceptual help topics
    Update-Help # Updates help files
    ```

## Basic Cmdlets

*   **Navigation**:
    *   Get current location:
        ```powershell
        Get-Location # Alias: gl, pwd
        ```
    *   Set current location (change directory):
        ```powershell
        Set-Location C:\Windows # Alias: sl, cd
        Set-Location .. # Parent directory
        ```
    *   List items in a location (files and directories):
        ```powershell
        Get-ChildItem # Alias: gci, ls, dir
        Get-ChildItem -Path C:\Users -Force # Show hidden/system files
        Get-ChildItem -Recurse # List recursively
        ```
*   **File and Directory Operations**:
    *   Create a new item (file or directory):
        ```powershell
        New-Item -Path C:\Temp\MyFile.txt -ItemType File
        New-Item -Path C:\Temp\MyFolder -ItemType Directory
        ```
    *   Remove an item:
        ```powershell
        Remove-Item -Path C:\Temp\MyFile.txt # Alias: ri, rm, del
        Remove-Item -Path C:\Temp\MyFolder -Recurse # Remove directory and its contents
        ```
    *   Copy an item:
        ```powershell
        Copy-Item -Path C:\Source\File.txt -Destination C:\Target\ # Alias: cpi, cp, copy
        Copy-Item -Path C:\SourceFolder -Destination C:\TargetFolder -Recurse
        ```
    *   Move an item:
        ```powershell
        Move-Item -Path C:\Source\File.txt -Destination C:\Target\ # Alias: mi, mv, move
        ```
    *   Rename an item:
        ```powershell
        Rename-Item -Path C:\OldName.txt -NewName NewName.txt # Alias: rni, ren
        ```
    *   Get content of a file:
        ```powershell
        Get-Content -Path C:\MyFile.txt # Alias: gc, cat, type
        Get-Content -Path C:\MyFile.txt -Tail 5 # Get last 5 lines
        ```
    *   Set content of a file (overwrites):
        ```powershell
        Set-Content -Path C:\MyFile.txt -Value "Hello, PowerShell" # Alias: sc
        ```
    *   Add content to a file (appends):
        ```powershell
        Add-Content -Path C:\MyFile.txt -Value "Another line" # Alias: ac
        ```
    *   Test if a path exists:
        ```powershell
        Test-Path -Path C:\MyFile.txt # Returns $true or $false
        ```
*   **Process Management**:
    *   Get running processes:
        ```powershell
        Get-Process # Alias: gps, ps
        Get-Process -Name "chrome"
        ```
    *   Stop a process:
        ```powershell
        Stop-Process -Name "notepad" # Alias: spp, kill
        Stop-Process -Id 1234
        ```
    *   Start a process:
        ```powershell
        Start-Process notepad.exe # Alias: sap, start
        Start-Process chrome.exe -ArgumentList "www.example.com"
        ```
*   **Service Management**:
    *   Get services:
        ```powershell
        Get-Service # Alias: gsv
        Get-Service -Name "spooler"
        ```
    *   Stop a service:
        ```powershell
        Stop-Service -Name "spooler" # Alias: spsv
        ```
    *   Start a service:
        ```powershell
        Start-Service -Name "spooler" # Alias: sasv
        ```
    *   Restart a service:
        ```powershell
        Restart-Service -Name "spooler" # Alias: rsrv
        ```
    *   Set service properties (e.g., startup type):
        ```powershell
        Set-Service -Name "wuauserv" -StartupType Manual
        ```
*   **Event Log**:
    ```powershell
    Get-EventLog -LogName System -Newest 10 # Get latest 10 system events (Windows PowerShell)
    Get-WinEvent -LogName System -MaxEvents 10 # (PowerShell Core / modern Windows)
    ```

## Variables

*   **Declare and assign a variable** (starts with `$`):
    ```powershell
    $myVariable = "Hello, World!"
    $number = 123
    $myArray = 1, "two", 3.0
    $myHashtable = @{ Name = "Jules"; Age = 30 }
    ```
*   **Use a variable**:
    ```powershell
    Write-Host $myVariable
    Write-Host "The number is: $number"
    $myArray[1] # Access array element (output: "two")
    $myHashtable.Name # Access hashtable value (output: "Jules")
    ```
*   **Variable Scopes**: `Global:`, `Script:`, `Local:` (default)
    ```powershell
    $Global:companyName = "MyCorp"
    ```
*   **Special Variables (Automatic Variables)**:
    *   `$_` or `$PSItem`: Current object in the pipeline.
    *   `$null`: Null value.
    *   `$true`, `$false`: Boolean values.
    *   `$Error`: Array of error objects from recent commands.
    *   `$HOME`: User's home directory path.
    *   `$PROFILE`: Path to the current user's PowerShell profile script.
    *   `$PID`: Process ID of the current PowerShell session.

## Operators

*   **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulus)
*   **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
*   **Comparison**:
    *   `-eq` (Equal)
    *   `-ne` (Not equal)
    *   `-gt` (Greater than)
    *   `-ge` (Greater than or equal)
    *   `-lt` (Less than)
    *   `-le` (Less than or equal)
    *   `-like` (Wildcard comparison, e.g., `"*test*"`), `-notlike`
    *   `-match` (Regex match), `-notmatch`
    *   `-contains` (Collection contains a value), `-notcontains`
    *   `-in` (Value is in a collection), `-notin`
*   **Logical**:
    *   `-and`
    *   `-or`
    *   `-xor`
    *   `-not` or `!`
*   **Type**: `-is` (Is instance of type), `-isnot`
*   **Redirection**: `>` (overwrite), `>>` (append), `2>&1` (redirect error stream to success stream) - See `about_Redirection`.

## Control Flow

*   **If-ElseIf-Else**:
    ```powershell
    $num = 10
    if ($num -gt 0) {
        Write-Host "Positive"
    }
    elseif ($num -lt 0) {
        Write-Host "Negative"
    }
    else {
        Write-Host "Zero"
    }
    ```
*   **Switch**:
    ```powershell
    $day = "Monday"
    switch ($day) {
        "Monday"   { Write-Host "Start of the week" }
        "Friday"   { Write-Host "Almost weekend!" }
        "Saturday" { Write-Host "Weekend!" }
        "Sunday"   { Write-Host "Weekend!" }
        Default    { Write-Host "Mid-week" }
    }
    ```
    ```powershell
    # Switch with -Regex and -Wildcard
    $value = "TestFile123.txt"
    switch -Regex ($value) {
        "^\w+\.txt$" { "It's a text file" }
        "^\w+\.log$" { "It's a log file" }
    }
    ```
*   **Loops**:
    *   **ForEach-Object** (for pipeline input):
        ```powershell
        Get-Process | ForEach-Object { Write-Host "Process: $($_.Name)" } # Alias: foreach, %
        ```
    *   **foreach** (looping through a collection):
        ```powershell
        $numbers = 1, 2, 3, 4, 5
        foreach ($n in $numbers) {
            Write-Host "Number: $n"
        }
        ```
    *   **For**:
        ```powershell
        for ($i = 1; $i -le 5; $i++) {
            Write-Host "For loop count: $i"
        }
        ```
    *   **While**:
        ```powershell
        $count = 0
        while ($count -lt 3) {
            Write-Host "While count: $count"
            $count++
        }
        ```
    *   **Do-While**:
        ```powershell
        $x = 0
        do {
            Write-Host "Do-While: $x"
            $x++
        } while ($x -lt 3)
        ```
    *   **Do-Until**:
        ```powershell
        $y = 0
        do {
            Write-Host "Do-Until: $y"
            $y++
        } until ($y -ge 3)
        ```
*   **Loop Control**: `break`, `continue`

## Functions

*   **Define a function**:
    ```powershell
    function Get-Greeting {
        param (
            [string]$Name = "User" # Parameter with default value
        )
        "Hello, $Name!"
    }
    ```
*   **Call a function**:
    ```powershell
    Get-Greeting -Name "Alice"
    Get-Greeting # Uses default value
    ```
*   **Advanced Functions (CmdletBinding)**:
    ```powershell
    function Test-ConnectionAdvanced {
        [CmdletBinding(SupportsShouldProcess=$true, ConfirmImpact='Medium')]
        param (
            [Parameter(Mandatory=$true, ValueFromPipeline=$true)]
            [string]$ComputerName,

            [int]$Count = 4
        )

        process { # Processes pipeline input
            if ($PSCmdlet.ShouldProcess($ComputerName, "Ping")) {
                Ping.exe -n $Count $ComputerName
            }
        }
    }
    ```
*   **Return values**: Functions return all uncaptured output. Use `return` for early exit or to clarify intent.

## Working with Objects

*   **Accessing properties**: `$object.PropertyName`
    ```powershell
    $proc = Get-Process -Name "powershell"
    Write-Host "PowerShell CPU usage: $($proc.CPU)"
    ```
*   **Calling methods**: `$object.MethodName()`
    ```powershell
    $myString = "hello"
    $myString.ToUpper() # Output: HELLO
    ```
*   **Filtering objects (Where-Object)**:
    ```powershell
    Get-Service | Where-Object {$_.Status -eq "Running"} # Alias: where, ?
    Get-Process | Where-Object Name -like "s*" # Simplified syntax for property comparison
    ```
*   **Selecting properties (Select-Object)**:
    ```powershell
    Get-Process | Select-Object -Property Name, Id, CPU # Alias: select
    Get-Process | Select-Object -First 5
    Get-Process | Select-Object -Property Name, @{Name="CPU_Seconds"; Expression={$_.CPU}} # Calculated property
    ```
*   **Sorting objects (Sort-Object)**:
    ```powershell
    Get-Process | Sort-Object -Property CPU -Descending # Alias: sort
    ```
*   **Grouping objects (Group-Object)**:
    ```powershell
    Get-Service | Group-Object -Property Status # Alias: group
    ```
*   **Measuring objects (Measure-Object)**:
    ```powershell
    Get-ChildItem C:\Windows\System32\*.dll | Measure-Object -Property Length -Sum -Average # Alias: measure
    ```

## Formatting Output

*   **Format-List**: Displays properties as a list.
    ```powershell
    Get-Process -Name "powershell" | Format-List * # Alias: fl
    ```
*   **Format-Table**: Displays properties in a table.
    ```powershell
    Get-Service | Format-Table Name, Status, DisplayName -AutoSize # Alias: ft
    ```
*   **Format-Wide**: Displays a single property in multiple columns.
    ```powershell
    Get-Command | Format-Wide Name -Column 5 # Alias: fw
    ```
*   **ConvertTo- (Data formats)**:
    ```powershell
    Get-Process | ConvertTo-Json
    Get-Service | ConvertTo-Csv -NoTypeInformation
    Get-ChildItem | ConvertTo-Html -Property Name, Length | Out-File report.html
    ```
*   **Out-File**: Sends output to a file.
    ```powershell
    Get-Process | Out-File -FilePath C:\Temp\processes.txt
    ```
*   **Out-GridView**: Sends output to an interactive table window.
    ```powershell
    Get-Process | Out-GridView
    ```

## Scripts (`.ps1` files)

*   **Execution Policy**: Controls script execution.
    *   `Get-ExecutionPolicy`
    *   `Set-ExecutionPolicy RemoteSigned` (Common setting; allows local scripts and signed remote scripts)
    *   Run a script bypassing policy (for current session): `powershell.exe -ExecutionPolicy Bypass -File .\MyScript.ps1`
*   **Parameters in scripts**:
    ```powershell
    # MyScript.ps1
    param (
        [string]$ComputerName = "localhost",
        [switch]$Force
    )
    Write-Host "Computer: $ComputerName, Force: $Force"
    ```
    ```powershell
    # Calling the script
    # .\MyScript.ps1 -ComputerName SERVER01 -Force
    ```
*   **Error Handling**:
    *   `Try-Catch-Finally`:
        ```powershell
        try {
            $result = 1 / 0
        }
        catch [System.DivideByZeroException] {
            Write-Error "Caught a DivideByZeroException: $($_.Exception.Message)"
        }
        catch { # Catch all other errors
            Write-Error "An unexpected error occurred: $($_.Exception.Message)"
        }
        finally {
            Write-Host "Cleanup operations here."
        }
        ```
    *   `Trap`: Less common, statement-level error handling.
    *   `$ErrorActionPreference`: Variable controlling default error behavior (`SilentlyContinue`, `Stop`, `Continue` (default), `Inquire`).

## Remoting

*   **Enable PSRemoting (on remote machine, as Admin)**:
    ```powershell
    Enable-PSRemoting -Force
    ```
*   **Enter an interactive session**:
    ```powershell
    Enter-PSSession -ComputerName SERVER01 # Alias: etsn
    # Exit session with 'Exit-PSSession' or 'exit'
    ```
*   **Invoke a command remotely**:
    ```powershell
    Invoke-Command -ComputerName SERVER01, SERVER02 -ScriptBlock { Get-Service -Name "spooler" } # Alias: icm
    Invoke-Command -ComputerName SERVER01 -FilePath C:\Scripts\MyLocalScript.ps1
    ```
*   **Persistent Sessions (PSSession)**:
    ```powershell
    $session = New-PSSession -ComputerName SERVER01
    Invoke-Command -Session $session -ScriptBlock { $remoteVar = "Hello from remote" }
    Invoke-Command -Session $session -ScriptBlock { Write-Host $remoteVar }
    Remove-PSSession $session
    ```

## Modules

*   **Find available modules**:
    ```powershell
    Get-Module -ListAvailable
    ```
*   **Import a module into current session**:
    ```powershell
    Import-Module ActiveDirectory
    Import-Module Pester -PassThru # Shows imported commands
    ```
*   **Find commands in a module**:
    ```powershell
    Get-Command -Module ActiveDirectory
    ```
*   **Install modules from PowerShell Gallery (requires PowerShellGet module)**:
    ```powershell
    Find-Module -Name "PSScriptAnalyzer"
    Install-Module -Name "PSScriptAnalyzer" -Scope CurrentUser # Install for current user
    Update-Module -Name "PSScriptAnalyzer"
    ```
*   **Module Auto-Loading**: PowerShell 5+ automatically loads modules when a command from them is called.
