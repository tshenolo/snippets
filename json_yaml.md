# JSON/YAML Cheatsheet

*   **JSON (JavaScript Object Notation)**:
    *   Syntax:
        *   Objects: `{ "key": "value", "number": 123, "nested": { ... } }` (Keys are strings).
        *   Arrays: `[ "apple", "banana", 100, { "object_in_array": true } ]`.
        *   Values: Strings (double-quoted), numbers, booleans (`true`, `false`), arrays, objects, `null`.
    *   Data Types: String, Number, Boolean, Array, Object, Null.
    *   Usage: Data interchange format, configuration files, APIs.
    *   Transformation Examples:
        *   Parsing (string to object): `JSON.parse()` (JavaScript), `json.loads()` (Python).
        *   Stringifying (object to string): `JSON.stringify()` (JavaScript), `json.dumps()` (Python).
*   **YAML (YAML Ain't Markup Language)**:
    *   Syntax: Human-readable data serialization standard. Uses indentation to denote structure.
        *   Key-Value Pairs: `key: value`
        *   Lists (Sequences):
            ```yaml
            - item1
            - item2
            - sublist:
              - subitemA
            ```
        *   Dictionaries (Mappings):
            ```yaml
            person:
              name: John Doe
              age: 30
            ```
        *   Scalars: Strings (can be unquoted, single-quoted, or double-quoted), numbers, booleans (`true`, `false`, `yes`, `no`, `on`, `off`).
        *   Comments: `# This is a comment`.
        *   Anchors (`&`) and Aliases (`*`): For reusing parts of the document.
        *   Multi-line Strings: `|` (literal, preserves newlines), `>` (folded, converts newlines to spaces).
    *   Usage: Configuration files (Docker Compose, Kubernetes, Ansible), data serialization.
    *   Transformation Examples (Python with PyYAML):
        *   Loading (YAML string/file to Python object): `yaml.safe_load()`.
        *   Dumping (Python object to YAML string): `yaml.dump()`.
    *   Comparison with JSON: YAML is often considered more readable for humans, supports comments, anchors/aliases. JSON is stricter and often faster for machines to parse.
