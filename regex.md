# Regex (Regular Expressions) Cheatsheet

*   **Purpose**: Pattern matching in text.
*   **Basic Metacharacters**:
    *   `.`: Any single character (except newline).
    *   `^`: Start of string/line.
    *   `$`: End of string/line.
    *   `*`: Zero or more of the preceding character/group.
    *   `+`: One or more of the preceding character/group.
    *   `?`: Zero or one of the preceding character/group (also for non-greedy matching).
    *   `\`: Escape character (e.g., `\.` matches a literal dot).
*   **Character Classes**:
    *   `[abc]`: Matches 'a', 'b', or 'c'.
    *   `[^abc]`: Matches any character except 'a', 'b', or 'c'.
    *   `[a-z]`: Matches any lowercase letter.
    *   `[0-9]`: Matches any digit.
    *   Predefined: `\d` (digit), `\D` (non-digit), `\s` (whitespace), `\S` (non-whitespace), `\w` (word char: alphanumeric + `_`), `\W` (non-word char).
*   **Quantifiers**:
    *   `{n}`: Exactly n times.
    *   `{n,}`: At least n times.
    *   `{n,m}`: Between n and m times.
    *   Greedy vs. Non-greedy (Lazy): `*?`, `+?`, `??`, `{n,}?`.
*   **Groups and Capturing**:
    *   `(pattern)`: Captures the matched substring.
    *   `(?:pattern)`: Non-capturing group.
    *   Backreferences: `\1`, `\2` refer to captured groups.
*   **Alternation**: `|` (OR operator, e.g., `cat|dog`).
*   **Anchors and Boundaries**: `\b` (word boundary), `\B` (non-word boundary).
*   **Lookahead/Lookbehind (Assertions)**:
    *   Positive Lookahead: `(?=pattern)`
    *   Negative Lookahead: `(?!pattern)`
    *   Positive Lookbehind: `(?<=pattern)`
    *   Negative Lookbehind: `(?<!pattern)`
*   **Flags/Modifiers** (depend on implementation, e.g., in Python `re` module):
    *   `i`: Case-insensitive.
    *   `g`: Global match (in tools like `sed`, JavaScript).
    *   `m`: Multiline (`^` and `$` match start/end of lines).
*   **Common Expressions**:
    *   Email: (complex, many variations, simple example: `^\S+@\S+\.\S+$`)
    *   URL: (complex, simple example: `^(https?|ftp)://[^\s/$.?#].[^\s]*$`)
    *   IP Address: `^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$`
    *   Date (YYYY-MM-DD): `^\d{4}-\d{2}-\d{2}$`
