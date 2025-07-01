# Regex (Regular Expressions) Cheatsheet

Regular expressions are sequences of characters that define a search pattern. They are used for pattern matching and "search-and-replace" operations on strings.

## Basic Metacharacters & Literals

*   **Literal Characters**: Ordinary characters match themselves.
    *   Example: `/cat/` matches "cat" in "The cat sat on the mat."
*   **`.` (Dot)**: Matches any single character (except newline, unless `s` flag is used).
    *   Example: `/c.t/` matches "cat", "cot", "c@t", etc.
*   **`^` (Caret)**: Matches the beginning of a string or line (if `m` flag is used).
    *   Example: `/^Hello/` matches "Hello" in "Hello World", but not in "World, Hello".
*   **`$` (Dollar)**: Matches the end of a string or line (if `m` flag is used).
    *   Example: `/end$/` matches "end" in "This is the end", but not in "end of the story".
*   **`\` (Backslash)**: Escapes a metacharacter, treating it as a literal. Or, creates a special character sequence.
    *   Example: `/^\[\d+\]$/` matches a string that starts with `[`, followed by one or more digits, and ends with `]`. (e.g., `[123]`)
    *   Example: `/\./` matches a literal dot ".".

## Character Classes (Sets) `[...]`

Match any one character from the set.
*   **`[abc]`**: Matches 'a', 'b', or 'c'.
    *   Example: `/[bcr]at/` matches "bat", "cat", or "rat".
*   **`[^abc]` (Negated Set)**: Matches any character *except* 'a', 'b', or 'c'.
    *   Example: `/[^0-9]/` matches any non-digit character.
*   **`[a-z]`**: Matches any lowercase letter from 'a' to 'z'.
    *   Example: `/[a-z]*/` matches zero or more lowercase letters.
*   **`[A-Z]`**: Matches any uppercase letter.
*   **`[0-9]`**: Matches any digit.
*   **Combinations**: `[a-zA-Z0-9_]` matches any alphanumeric character or underscore (equivalent to `\w`).

## Predefined Character Classes

*   **`\d`**: Matches any digit. Equivalent to `[0-9]`.
*   **`\D`**: Matches any non-digit character. Equivalent to `[^0-9]`.
*   **`\s`**: Matches any whitespace character (space, tab, newline, form feed, vertical tab). Equivalent to `[ \t\n\r\f\v]`.
*   **`\S`**: Matches any non-whitespace character. Equivalent to `[^ \t\n\r\f\v]`.
*   **`\w`**: Matches any "word" character (alphanumeric characters plus underscore). Equivalent to `[a-zA-Z0-9_]`.
*   **`\W`**: Matches any non-word character. Equivalent to `[^a-zA-Z0-9_]`.

## Quantifiers

Specify how many times the preceding character, group, or character class must occur.
*   **`*` (Asterisk)**: Matches zero or more occurrences. Greedy.
    *   Example: `/colou*r/` matches "color", "colour".
    *   Example: `/a*b/` matches "b", "ab", "aaab".
*   **`+` (Plus)**: Matches one or more occurrences. Greedy.
    *   Example: `/go+gle/` matches "gogle", "google".
    *   Example: `/a+b/` matches "ab", "aaab", but not "b".
*   **`?` (Question Mark)**: Matches zero or one occurrence. Greedy.
    *   Example: `/favou?rite/` matches "favorite", "favourite".
*   **`{n}`**: Matches exactly `n` occurrences.
    *   Example: `/\d{3}/` matches exactly three digits (e.g., "123").
*   **`{n,}`**: Matches at least `n` occurrences. Greedy.
    *   Example: `/\d{2,}/` matches two or more digits.
*   **`{n,m}`**: Matches between `n` and `m` occurrences (inclusive). Greedy.
    *   Example: `/\w{3,5}/` matches three, four, or five word characters.

*   **Lazy Quantifiers** (Non-Greedy): Add a `?` after the quantifier to make it lazy (match as few characters as possible).
    *   `*?`: Zero or more, lazy. Example: `/<p>.*?<\/p>/` matches `<p>text</p>` without overmatching if multiple `<p>` tags exist.
    *   `+?`: One or more, lazy.
    *   `??`: Zero or one, lazy (rarely different from greedy `?`).
    *   `{n,}?`: At least n, lazy.
    *   `{n,m}?`: Between n and m, lazy.

## Groups and Capturing `(...)`

*   **`(pattern)` (Capturing Group)**: Groups a part of the pattern and captures the matched substring. Captured groups can be referenced by number (e.g., `\1`, `\2`) or used in replacements (e.g., `$1`, `$2`).
    *   Example: `/(\w+) (\w+)/` captures two words. In "John Doe", `\1` is "John", `\2` is "Doe".
*   **`(?:pattern)` (Non-Capturing Group)**: Groups a part of the pattern for quantifiers or alternation, but does not capture the match.
    *   Example: `/(?:com|org|net)/` matches "com", "org", or "net" without creating a capture group.
*   **Backreferences `\1`, `\2`, ...**: Refer to previously captured groups within the same regex.
    *   Example: `/(\w+)\s+\1/` matches repeated words like "hello hello". `\1` refers to the text matched by the first capturing group.
*   **Named Capturing Groups `(?<name>pattern)`** (syntax varies by engine, this is common):
    *   Example: `/(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/`
    *   Reference by name: `\k<name>` in some engines or used in replacement logic.

## Alternation `|` (OR)

Matches either the pattern before or the pattern after the `|`.
*   Example: `/cat|dog|fish/` matches "cat", "dog", or "fish".
*   Use grouping for more complex alternation: `/^(apple|banana) pie$/` matches "apple pie" or "banana pie".

## Anchors and Boundaries

*   **`^`**: Start of string/line.
*   **`$`**: End of string/line.
*   **`\b` (Word Boundary)**: Matches a position between a word character (`\w`) and a non-word character (`\W`), or start/end of string if the first/last character is a word character.
    *   Example: `/\bcat\b/` matches "cat" in "The cat sat." but not in "catalog" or "concatenate".
*   **`\B` (Non-Word Boundary)**: Matches a position that is not a word boundary.
    *   Example: `/\Bcat\B/` matches "cat" in "concatenate" but not in "cat" or "the cat".
*   **`\A`**: Start of the entire string (not affected by multiline mode in some engines like Perl, Python).
*   **`\Z`**: End of the entire string (not affected by multiline mode in some engines like Perl, Python; may match before a final newline).
*   **`\z`**: Absolute end of the string (Perl, Python).

## Lookahead and Lookbehind Assertions (Zero-Width Assertions)

These check for patterns without including them in the actual match.
*   **`(?=pattern)` (Positive Lookahead)**: Asserts that `pattern` follows the current position, but doesn't consume characters.
    *   Example: `/Windows(?= 95|98|NT|XP)/` matches "Windows" only if it's followed by " 95", " 98", " NT", or " XP". The " 95" etc. is not part of the match.
*   **`(?!pattern)` (Negative Lookahead)**: Asserts that `pattern` does *not* follow the current position.
    *   Example: `/apple(?! pie)/` matches "apple" if it's not followed by " pie". Matches "apple" in "apple juice".
*   **`(?<=pattern)` (Positive Lookbehind)**: Asserts that `pattern` precedes the current position. (Not supported in all regex engines, or with limitations like fixed-length patterns).
    *   Example: `/(?<=USD)\d+/` matches digits only if they are preceded by "USD". Matches "100" in "USD100".
*   **`(?<!pattern)` (Negative Lookbehind)**: Asserts that `pattern` does *not* precede the current position. (Similar limitations as positive lookbehind).
    *   Example: `/(?<!non-)\w+ful/` matches words ending in "ful" that are not preceded by "non-". Matches "beautiful" but not "non-eventful".

## Flags (Modifiers)

Flags change how the regex engine interprets the pattern. Syntax for flags varies (e.g., `/pattern/flags` in JavaScript/Perl, `re.compile(pattern, flags)` in Python).
*   **`i` (Case-Insensitive)**: Makes the match case-insensitive.
    *   Example: `/apple/i` matches "apple", "Apple", "APPLE".
*   **`g` (Global)**: Finds all matches rather than stopping after the first match. (Primarily relevant in contexts like JavaScript's `replace` or `matchAll`).
*   **`m` (Multiline)**: `^` and `$` match the start and end of each line (delimited by `\n` or `\r`) instead of just the start and end of the entire string.
*   **`s` (Dotall or Single Line)**: Allows `.` (dot) to match newline characters as well.
*   **`u` (Unicode)**: Enables more complete Unicode support, including matching characters outside the Basic Multilingual Plane (e.g., some emojis).
*   **`x` (Extended/Verbose)**: Allows whitespace and comments within the regex pattern for readability (whitespace is ignored, `#` starts a comment).
    *   Example (Python):
        ```python
        # import re
        # pattern = re.compile(r"""
        #    \d{3}     # Match three digits
        #    -         # Match a hyphen
        #    \d{4}     # Match four digits
        # """, re.VERBOSE)
        ```

## Common Regex Patterns (Examples)

*   **Match an Integer**: `^-?\d+$`
*   **Match a Floating Point Number**: `^-?\d*\.\d+$` or `^-?\d+(\.\d+)?$` (more robust needed for various formats)
*   **Match a North American Phone Number**: `^\(?([2-9]\d{2})\)?[-.\s]?([2-9]\d{2})[-.\s]?(\d{4})$`
*   **Match an Email Address (Simplified)**: `^\S+@\S+\.\S+$`
    *   *Note: A truly RFC 5322 compliant email regex is extremely complex.*
*   **Match a URL (Simplified)**: `^(https?|ftp):\/\/[^\s/$.?#].[^\s]*$`
*   **Match a Date (YYYY-MM-DD)**: `^\d{4}-\d{2}-\d{2}$` or `^(19|20)\d\d-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01])$` (more specific)
*   **Match an IPv4 Address**: `^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$`
*   **Match Hex Color Code**: `^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$`
*   **Extract all words from a string**: `\b\w+\b` (used with a global flag or iteration)
*   **Validate a password** (e.g., min 8 chars, at least one uppercase, one lowercase, one digit):
    `^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d\S]{8,}$`
    *   `(?=.*[a-z])`: Positive lookahead for a lowercase letter.
    *   `(?=.*[A-Z])`: Positive lookahead for an uppercase letter.
    *   `(?=.*\d)`: Positive lookahead for a digit.
    *   `[a-zA-Z\d\S]{8,}`: Matches 8 or more alphanumeric or non-whitespace special characters.

**Regex Testers**: Tools like regex101.com, regextester.com, or integrated IDE features are invaluable for testing and debugging regular expressions.

This provides a comprehensive Regex cheatsheet. I'll proceed with `json_yaml.md`.The `regex.md` cheatsheet has been successfully updated with detailed explanations and examples for metacharacters, character classes, quantifiers, groups, assertions, flags, and common regex patterns.

Next, I will enhance `json_yaml.md`. This will involve providing clearer examples of JSON and YAML syntax, data types, and common transformation or parsing examples in pseudocode or common languages like Python/JavaScript.
