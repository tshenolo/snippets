# PowerShell Cheatsheet

*   **Core Concepts**: Cmdlets (verb-noun, e.g., `Get-Process`), Objects, Pipeline (`|`).
*   **Basic Cmdlets**:
    *   Navigation: `Get-Location` (`pwd`), `Set-Location` (`cd`), `Get-ChildItem` (`ls`, `dir`).
    *   File/Directory: `New-Item`, `Remove-Item`, `Copy-Item`, `Move-Item`, `Get-Content`, `Set-Content`, `Add-Content`.
    *   Process: `Get-Process`, `Stop-Process`, `Start-Process`.
    *   Service: `Get-Service`, `Stop-Service`, `Start-Service`, `Set-Service`.
*   **Variables**: `$variableName = "value"`.
*   **Operators**: Comparison (`-eq`, `-ne`, `-gt`, `-lt`, `-like`, `-match`), Logical (`-and`, `-or`, `-not`).
*   **Control Flow**:
    *   `If (-ElseIf / -Else)`: `if ($condition) { ... } elseif ($condition2) { ... } else { ... }`
    *   `Switch`: `switch ($value) { value1 {...} default {...} }`
    *   Loops: `ForEach-Object` (alias `%`), `foreach ($item in $collection) { ... }`, `For`, `While`, `Do-While/Until`.
*   **Functions**: `function Function-Name { Param($param1, $param2) ... }`.
*   **Working with Objects**: Accessing properties (`$object.PropertyName`), methods (`$object.MethodName()`).
*   **Filtering and Selecting**: `Where-Object` (alias `?`), `Select-Object` (alias `select`).
*   **Formatting Output**: `Format-List`, `Format-Table`, `ConvertTo-Csv`, `ConvertTo-Json`, `Out-File`.
*   **Scripts (`.ps1` files)**: Execution policy (`Set-ExecutionPolicy`), parameters.
*   **Remoting**: `Enter-PSSession`, `Invoke-Command`.
*   **Modules**: `Import-Module`, `Get-Module`.
