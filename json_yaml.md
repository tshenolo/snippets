# JSON & YAML Cheatsheet

This cheatsheet covers the syntax, data types, and common usage patterns for JSON (JavaScript Object Notation) and YAML (YAML Ain't Markup Language).

## JSON (JavaScript Object Notation)

JSON is a lightweight data-interchange format. It is easy for humans to read and write and easy for machines to parse and generate. JSON is built on two structures:
*   A collection of name/value pairs (e.g., an object, record, struct, dictionary, hash table, keyed list, or associative array).
*   An ordered list of values (e.g., an array, vector, list, or sequence).

*   **Syntax Rules**:
    *   Data is in name/value pairs.
    *   Data is separated by commas.
    *   Curly braces `{}` hold objects.
    *   Square brackets `[]` hold arrays.
    *   Keys (names) must be strings in double quotes (`"`).
    *   Values must be a valid JSON data type (string, number, object, array, boolean, or `null`).
    *   No comments are allowed in standard JSON.

*   **Data Types**:
    *   **String**: Sequence of Unicode characters in double quotes. Backslash `\` is used for escaping special characters (e.g., `\"`, `\\`, `\n`, `\t`).
        ```json
        "hello world",
        "line1\nline2"
        ```
    *   **Number**: Integer or floating-point. No distinction between them. Octal and hex formats are not allowed. `NaN` and `Infinity` are not valid JSON numbers.
        ```json
        100,
        -2.5,
        3.14159e10
        ```
    *   **Boolean**: `true` or `false` (lowercase).
        ```json
        true,
        false
        ```
    *   **Array**: Ordered list of values, enclosed in `[]`. Values can be of different types.
        ```json
        [1, "apple", true, null, {"nested_key": "nested_value"}]
        ```
    *   **Object**: Unordered collection of key/value pairs, enclosed in `{}`. Keys are strings.
        ```json
        {
            "name": "John Doe",
            "age": 30,
            "isStudent": false,
            "address": {
                "street": "123 Main St",
                "city": "Anytown"
            },
            "courses": ["Math", "History"]
        }
        ```
    *   **`null`**: Represents an empty value or no value (lowercase).
        ```json
        null
        ```

*   **Example JSON Document**:
    ```json
    {
      "id": "user123",
      "username": "johndoe",
      "email": "john.doe@example.com",
      "isActive": true,
      "roles": ["user", "editor"],
      "profile": {
        "firstName": "John",
        "lastName": "Doe",
        "age": null,
        "avatarUrl": "https://example.com/avatars/johndoe.png"
      },
      "metadata": [
        {"key": "lastLogin", "value": "2023-10-26T10:00:00Z"},
        {"key": "theme", "value": "dark"}
      ]
    }
    ```

*   **Transformation/Parsing Examples**:
    *   **JavaScript**:
        ```javascript
        // Parsing JSON string to JavaScript object
        const jsonString = '{"name":"Alice","age":25}';
        const jsObject = JSON.parse(jsonString);
        console.log(jsObject.name); // Output: Alice

        // Converting JavaScript object to JSON string
        const person = { name: "Bob", city: "London" };
        const jsonOutput = JSON.stringify(person, null, 2); // null, 2 for pretty-printing with 2 spaces
        console.log(jsonOutput);
        /* Output:
        {
          "name": "Bob",
          "city": "London"
        }
        */
        ```
    *   **Python**:
        ```python
        import json

        # Parsing JSON string to Python dictionary
        json_string_py = '{"name":"Charlie","isStudent":true}'
        py_dict = json.loads(json_string_py)
        print(py_dict['name']) # Output: Charlie

        # Converting Python dictionary to JSON string
        data_py = {'id': 1, 'items': ['item1', 'item2'], 'valid': None} # Python None becomes JSON null
        json_output_py = json.dumps(data_py, indent=4) # indent=4 for pretty-printing
        print(json_output_py)
        """Output:
        {
            "id": 1,
            "items": [
                "item1",
                "item2"
            ],
            "valid": null
        }
        """
        ```

## YAML (YAML Ain't Markup Language)

YAML is a human-friendly data serialization standard for all programming languages. It is often used for configuration files and in applications where data is being stored or transmitted. YAML is a superset of JSON; valid JSON is also valid YAML (mostly).

*   **Syntax Rules**:
    *   Indentation (spaces, not tabs) is used to denote structure. Consistent indentation is crucial.
    *   Comments start with `#`.
    *   Sequences (arrays/lists) are denoted by a dash and space (`- `).
    *   Mappings (objects/dictionaries) are represented as key-value pairs (`key: value`).
    *   Strings usually don't require quotes, but can be quoted (`'` or `"`).
    *   Multiple documents in a single file are separated by `---`. An optional `...` can end a document.

*   **Data Types (Scalars and Collections)**:
    *   **Scalars** (basic values):
        *   **Strings**:
            ```yaml
            my_string: This is a plain string
            another_string: "A string in double quotes, can use \n escapes"
            single_quoted: 'A string in single quotes, escapes like \n are literal, '' is a single quote'
            multiline_literal: |
              This is line one.
              This is line two.
              Indentation is preserved.
            multiline_folded: >
              This text will be folded
              into a single paragraph.
              Blank lines indicate new paragraphs.

              This is a new paragraph.
            ```
        *   **Numbers**: Integers and floats.
            ```yaml
            count: 123
            pi: 3.14159
            scientific: 1.23e+5
            hexadecimal: 0xFF # 255
            octal: 0o12 # 10 (YAML 1.2+)
            ```
        *   **Booleans**: `true`, `false` (also `yes`, `no`, `on`, `off` are often supported but `true`/`false` are canonical).
            ```yaml
            is_enabled: true
            is_valid: no # often parsed as false
            ```
        *   **Null**: `null` or `~` (tilde). Leaving a value blank also implies null.
            ```yaml
            empty_value: null
            another_empty: ~
            yet_another_empty:
            ```
        *   **Dates and Timestamps** (ISO 8601 format):
            ```yaml
            date: 2023-10-27
            datetime: 2023-10-27T14:30:00Z # Z for UTC
            timestamp: 2023-10-27 10:30:00 -05:00 # With timezone offset
            ```
    *   **Collections**:
        *   **Sequences (Lists/Arrays)**: Elements are denoted by a leading hyphen and space (`- `).
            ```yaml
            fruits:
              - Apple
              - Banana
              - Cherry
            # Inline sequence (flow style)
            colors: [red, green, blue]
            ```
        *   **Mappings (Dictionaries/Objects)**: Key-value pairs.
            ```yaml
            person:
              name: John Doe
              age: 30
              isStudent: false
              address: # Nested mapping
                street: 123 Main St
                city: Anytown
            # Inline mapping (flow style)
            contact: { email: "john@example.com", phone: "555-1234" }
            ```

*   **Example YAML Document**:
    ```yaml
    # This is a comment
    application:
      name: My Awesome App
      version: 1.2.3
      environment: production
      debug_mode: false
      database:
        adapter: postgresql
        host: db.example.com
        port: 5432
        username: app_user
        # Password should ideally be handled via secrets management, not plain text
        # password: "securepassword"
      features_enabled:
        - user_auth
        - notifications
        - reporting
      contact_info:
        email: support@example.com
        phone: null # Explicitly null
        office_hours: >
          Monday to Friday,
          9 AM to 5 PM.
          Closed on public holidays.
      metadata:
        - key: owner
          value: "Admin Team"
        - key: last_updated
          value: 2023-10-27T12:00:00Z
    ---
    # Second document (optional)
    another_config:
      setting: value
    ```

*   **Advanced Features**:
    *   **Anchors (`&`) and Aliases (`*`)**: For reusing parts of the document (DRY - Don't Repeat Yourself).
        ```yaml
        defaults: &default_user_prefs
          theme: dark
          notifications: true

        user1:
          name: Alice
          preferences: *default_user_prefs

        user2:
          name: Bob
          preferences:
            <<: *default_user_prefs # Merge an alias
            notifications: false # Override a specific value
            language: en
        ```
    *   **Tags**: Explicitly specify the type of a node (e.g., `!!str`, `!!int`, `!!map`, custom tags `!mytype`).
        ```yaml
        explicit_string: !!str 123 # Treat 123 as a string
        explicit_int: !!int "42"  # Treat "42" as an integer
        ```

*   **Transformation/Parsing Examples**:
    *   **Python (using `PyYAML` library)**:
        ```bash
        # pip install PyYAML
        ```
        ```python
        import yaml

        yaml_string = """
        name: Eve
        age: 28
        city: London
        skills:
          - Python
          - Docker
        """
        # Load YAML string to Python dictionary
        try:
            data = yaml.safe_load(yaml_string) # safe_load is recommended over load
            print(data['name']) # Output: Eve
            print(data['skills'][0]) # Output: Python
        except yaml.YAMLError as e:
            print(f"Error parsing YAML: {e}")

        # Dump Python dictionary to YAML string
        py_object = {
            'id': 'item001',
            'price': 49.99,
            'tags': ['electronics', 'audio'],
            'available': True
        }
        yaml_output = yaml.dump(py_object, sort_keys=False) # sort_keys=False to maintain order
        print(yaml_output)
        """Output:
        id: item001
        price: 49.99
        tags:
        - electronics
        - audio
        available: true
        """
        ```
    *   **JavaScript (using `js-yaml` library - typically in Node.js or with a bundler)**:
        ```bash
        # npm install js-yaml
        ```
        ```javascript
        // const yaml = require('js-yaml'); // CommonJS
        // import yaml from 'js-yaml'; // ES Module

        // const yamlStringJs = `
        //   user:
        //     name: Charlie
        //     active: true
        //   permissions: [read, write]
        // `;

        // try {
        //   const doc = yaml.load(yamlStringJs);
        //   console.log(doc.user.name); // Output: Charlie
        // } catch (e) {
        //   console.error("Error parsing YAML:", e);
        // }

        // const jsData = {
        //   service: "auth-service",
        //   version: "v2",
        //   replicas: 3
        // };
        // const yamlOutputJs = yaml.dump(jsData);
        // console.log(yamlOutputJs);
        /* Output:
        service: auth-service
        version: v2
        replicas: 3
        */
        ```

## JSON vs YAML Key Differences

| Feature         | JSON                                  | YAML                                                |
|-----------------|---------------------------------------|-----------------------------------------------------|
| **Readability** | Good for machines, okay for humans    | Excellent for humans, good for machines             |
| **Comments**    | Not allowed                           | Allowed (`#`)                                       |
| **Syntax**      | Stricter, more verbose (quotes, braces) | More concise, uses indentation, less punctuation    |
| **Data Types**  | Strings, numbers, booleans, arrays, objects, null | Richer scalars (dates, multiline strings), collections |
| **Advanced**    | None (simple structure)               | Anchors, aliases, tags, multiple documents          |
| **Superset**    | No (YAML is mostly a superset of JSON)| Yes (most valid JSON is valid YAML)                 |
| **Use Cases**   | APIs, data interchange, simple configs| Configuration files, data serialization, inter-process messaging |

Choose JSON for strict data interchange where simplicity and broad machine compatibility are key.
Choose YAML for configuration files and situations where human readability and more advanced structuring features (like comments and anchors) are beneficial.

This provides a comprehensive JSON & YAML cheatsheet. I'll proceed with `gpg_encryption.md`.The `json_yaml.md` cheatsheet has been successfully updated with detailed explanations of syntax, data types, example documents, and common parsing/transformation snippets in JavaScript and Python for both JSON and YAML. Key differences are also highlighted.

Next, I will enhance `gpg_encryption.md`, focusing on providing clear command examples for key management, encryption, decryption, signing, and verification.
