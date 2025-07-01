## Cheatsheets

Here is a collection of cheatsheets categorized for easy access.

**💻 Programming Languages**

*   ### [Python](python.md)
    *   Basic Syntax: Variables, Data Types (strings, integers, floats, booleans, lists, tuples, dictionaries, sets), Operators.
    *   Control Flow: If/elif/else, for loops, while loops, break, continue.
    *   Functions: Defining functions, arguments (positional, keyword, `*args`, `**kwargs`), return values, lambdas.
    *   List Comprehensions: Syntax, examples with conditions.
    *   Decorators: Basic syntax (`@decorator`), `functools.wraps`.
    *   Object-Oriented Programming: Classes, objects, inheritance, encapsulation, polymorphism.
    *   Modules & Packages: Importing, creating modules.
    *   File I/O: Reading and writing files.
    *   Error Handling: Try/except/finally blocks.
    *   Common Standard Library Modules: `os`, `sys`, `datetime`, `json`, `re`.

*   ### [JavaScript (ES6+)](javascript.md)
    *   Basic Syntax: Variables (`let`, `const`, `var`), Data Types (string, number, boolean, object, array, null, undefined, symbol, bigint).
    *   Operators: Arithmetic, assignment, comparison, logical, ternary.
    *   Control Flow: `if/else`, `switch`, `for`, `while`, `do...while`.
    *   Functions: Declarations, expressions, arrow functions, parameters, `this` keyword.
    *   Arrays: Creation, `push`, `pop`, `shift`, `unshift`, `slice`, `splice`, `map`, `filter`, `reduce`, `forEach`, `find`, `includes`.
    *   Objects: Literals, properties, methods, destructuring, spread syntax.
    *   DOM Manipulation: Selecting elements (`getElementById`, `querySelector`), changing content/attributes, event listeners.
    *   ES6+ Features: Template literals, destructuring, default parameters, rest/spread operators, classes, modules (import/export), promises, async/await.

*   ### [TypeScript](typescript.md)
    *   Basic Types: `string`, `number`, `boolean`, `array` (`number[]` or `Array<number>`), `tuple`, `enum`, `any`, `void`, `null`, `undefined`, `never`, `object`.
    *   Interfaces: Defining shapes for objects, optional properties, readonly properties, function types, indexable types, class types.
    *   Classes: Syntax, constructors, properties, methods, inheritance, access modifiers (`public`, `private`, `protected`), abstract classes.
    *   Functions: Typed parameters, return types, optional and default parameters, rest parameters.
    *   Generics: Creating reusable components with type variables (functions, classes, interfaces).
    *   Type Inference: How TypeScript infers types.
    *   Type Compatibility: Structural typing.
    *   Advanced Types: Union types, intersection types, literal types, type guards, conditional types, mapped types.
    *   Modules: `export` and `import` syntax.
    *   Declaration Files (`.d.ts`): For external JavaScript libraries.

*   ### [Java](java.md)
    *   Basic Syntax: Variables, Data Types (primitive: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`; reference: objects, arrays).
    *   Operators: Arithmetic, relational, logical, assignment.
    *   Control Flow: `if/else`, `switch`, `for`, `while`, `do...while`, `break`, `continue`.
    *   Object-Oriented Programming (OOP):
        *   Classes and Objects: Declaration, instantiation, `this` keyword.
        *   Encapsulation: Access modifiers (`public`, `private`, `protected`, default).
        *   Inheritance: `extends` keyword, `super` keyword, polymorphism, method overriding.
        *   Abstraction: Abstract classes and methods, interfaces.
    *   Methods: Definition, parameters, return types, overloading.
    *   Arrays: Declaration, initialization, accessing elements.
    *   Strings: `String` class, common methods.
    *   Collections Framework:
        *   `List` (e.g., `ArrayList`, `LinkedList`): Ordered collections.
        *   `Set` (e.g., `HashSet`, `TreeSet`): Collections of unique elements.
        *   `Map` (e.g., `HashMap`, `TreeMap`): Key-value pairs.
    *   Streams API (Java 8+): `stream()`, intermediate operations (`filter`, `map`, `sorted`), terminal operations (`collect`, `forEach`, `reduce`).
    *   Exception Handling: `try-catch-finally` blocks, `throw`, `throws`.
    *   Packages: Organizing classes, `import` statements.

*   ### [PHP](php.md)
    *   Basic Syntax: Tags (`<?php ... ?>`), comments, variables (`$variable`), echo/print.
    *   Data Types: `string`, `integer`, `float`, `boolean`, `array`, `object`, `NULL`, `resource`.
    *   Operators: Arithmetic, assignment, comparison, logical, string concatenation (`.`).
    *   Control Structures: `if/elseif/else`, `switch`, `for`, `foreach`, `while`, `do...while`, `break`, `continue`.
    *   Functions: Defining functions, arguments (typed, default values, variable-length `...$args`), return types.
    *   Arrays:
        *   Indexed arrays: `[value1, value2]` or `array(value1, value2)`.
        *   Associative arrays: `['key1' => 'value1', 'key2' => 'value2']`.
        *   Common array functions: `count`, `sort`, `rsort`, `asort`, `ksort`, `array_push`, `array_pop`, `array_key_exists`, `in_array`, `array_merge`, `array_slice`.
    *   String Functions: `strlen`, `strpos`, `substr`, `str_replace`, `strtolower`, `strtoupper`, `trim`, `explode`, `implode`, `htmlspecialchars`.
    *   Superglobals: `$_GET`, `$_POST`, `$_REQUEST`, `$_SERVER`, `$_SESSION`, `$_COOKIE`.
    *   Object-Oriented Programming: Classes, objects, properties, methods, inheritance, visibility (`public`, `private`, `protected`), constructors, destructors, static members, namespaces.
    *   File Handling: `fopen`, `fread`, `fwrite`, `fclose`, `file_get_contents`, `file_put_contents`.
    *   Error Handling: `try/catch` blocks, `trigger_error`.

*   ### [PeopleCode](peoplecode.md)

**⚙️ Scripting & Automation**

*   ### [Bash](bash.md)
    *   Basic Commands: `ls`, `cd`, `pwd`, `mkdir`, `rm`, `cp`, `mv`, `cat`, `echo`, `grep`, `find`, `chmod`, `chown`.
    *   Variables: Declaration (`VAR="value"`), usage (`$VAR` or `${VAR}`).
    *   Command Substitution: `$(command)` or `` `command` ``.
    *   Arithmetic Expansion: `$((expression))`.
    *   Input/Output Redirection: `>`, `>>`, `<`, `2>`, `&>`, `|` (pipes).
    *   Loops:
        *   `for var in list; do ... done`
        *   `for (( expr1; expr2; expr3 )); do ... done` (C-style)
        *   `while condition; do ... done`
        *   `until condition; do ... done`
    *   Conditionals:
        *   `if condition; then ... elif condition; then ... else ... fi`
        *   Test command (`[ expression ]` or `[[ expression ]]`): File tests (`-f`, `-d`), string comparisons (`=`, `!=`, `-z`, `-n`), numerical comparisons (`-eq`, `-ne`, `-lt`, `-gt`).
        *   `case` statements.
    *   Functions: `function_name() { commands; }` or `function function_name { commands; }`, arguments (`$1`, `$2`, `$@`, `$*`), return status (`return code`).
    *   File Operations: Reading line by line, checking existence, permissions.
    *   Scripting Best Practices: Shebang (`#!/bin/bash`), comments, error handling (`set -e`, `set -u`, `set -o pipefail`), exit codes.

*   ### [Cron Jobs](cronjobs.md)
    *   Purpose: Scheduling commands or scripts to run periodically.
    *   Crontab File: User-specific (`crontab -e`), system-wide (`/etc/crontab`, `/etc/cron.d/`).
    *   Timing Syntax (5 fields + command):
        *   Minute (0-59)
        *   Hour (0-23)
        *   Day of Month (1-31)
        *   Month (1-12 or JAN-DEC)
        *   Day of Week (0-7 or SUN-SAT, where 0 and 7 are Sunday)
    *   Special Characters:
        *   `*`: Any value.
        *   `,`: Value list separator.
        *   `-`: Range of values.
        *   `/`: Step values (e.g., `*/15` for every 15 minutes).
    *   Special Strings (Macros): `@reboot`, `@yearly`, `@annually`, `@monthly`, `@weekly`, `@daily`, `@hourly`.
    *   Real Examples:
        *   Run a script every day at 2 AM: `0 2 * * * /path/to/script.sh`
        *   Run a command every 15 minutes: `*/15 * * * * /usr/bin/some_command`
        *   Run a script on the 1st of every month at midnight: `0 0 1 * * /path/to/monthly_report.sh`
        *   Run a script every Monday at 9 AM: `0 9 * * 1 /path/to/weekly_task.sh`
    *   Managing Cron Jobs: `crontab -l` (list), `crontab -r` (remove).
    *   Environment: Cron jobs run with a minimal environment; specify full paths to executables, manage `PATH` if needed.
    *   Logging Output: Redirect stdout and stderr (`> /path/to/logfile.log 2>&1`).

*   ### [PowerShell](powershell.md)
    *   Core Concepts: Cmdlets (verb-noun, e.g., `Get-Process`), Objects, Pipeline (`|`).
    *   Basic Cmdlets:
        *   Navigation: `Get-Location` (`pwd`), `Set-Location` (`cd`), `Get-ChildItem` (`ls`, `dir`).
        *   File/Directory: `New-Item`, `Remove-Item`, `Copy-Item`, `Move-Item`, `Get-Content`, `Set-Content`, `Add-Content`.
        *   Process: `Get-Process`, `Stop-Process`, `Start-Process`.
        *   Service: `Get-Service`, `Stop-Service`, `Start-Service`, `Set-Service`.
    *   Variables: `$variableName = "value"`.
    *   Operators: Comparison (`-eq`, `-ne`, `-gt`, `-lt`, `-like`, `-match`), Logical (`-and`, `-or`, `-not`).
    *   Control Flow:
        *   `If (-ElseIf / -Else)`: `if ($condition) { ... } elseif ($condition2) { ... } else { ... }`
        *   `Switch`: `switch ($value) { value1 {...} default {...} }`
        *   Loops: `ForEach-Object` (alias `%`), `foreach ($item in $collection) { ... }`, `For`, `While`, `Do-While/Until`.
    *   Functions: `function Function-Name { Param($param1, $param2) ... }`.
    *   Working with Objects: Accessing properties (`$object.PropertyName`), methods (`$object.MethodName()`).
    *   Filtering and Selecting: `Where-Object` (alias `?`), `Select-Object` (alias `select`).
    *   Formatting Output: `Format-List`, `Format-Table`, `ConvertTo-Csv`, `ConvertTo-Json`, `Out-File`.
    *   Scripts (`.ps1` files): Execution policy (`Set-ExecutionPolicy`), parameters.
    *   Remoting: `Enter-PSSession`, `Invoke-Command`.
    *   Modules: `Import-Module`, `Get-Module`.

*   ### [Linux](linux.md)
*   ### [Windows](windows.md)

**🌐 Web Development**

*   ### [HTML/CSS](html_css.md)
    *   HTML (Structure):
        *   Basic Document Structure: `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`.
        *   Head Elements: `<title>`, `<meta>`, `<link>` (for CSS), `<script>`.
        *   Common Body Tags: Headings (`<h1>` to `<h6>`), paragraphs (`<p>`), links (`<a>`), images (`<img>`), lists (`<ul>`, `<ol>`, `<li>`), divs (`<div>`), spans (`<span>`).
        *   Semantic HTML5: `<article>`, `<section>`, `<nav>`, `<aside>`, `<header>`, `<footer>`, `<main>`.
        *   Forms: `<form>`, `<input>` (types: text, password, checkbox, radio, submit, etc.), `<textarea>`, `<select>`, `<label>`.
    *   CSS (Styling & Layout):
        *   Selectors: Element, class (`.classname`), ID (`#idname`), attribute, pseudo-class (`:hover`), pseudo-element (`::before`).
        *   Properties: `color`, `background-color`, `font-size`, `font-family`, `width`, `height`, `padding`, `margin`, `border`.
        *   Box Model: Content, padding, border, margin.
        *   Layout:
            *   Display Property: `block`, `inline`, `inline-block`, `none`, `flex`, `grid`.
            *   Positioning: `static`, `relative`, `absolute`, `fixed`, `sticky`.
            *   Flexbox: Container (`display: flex`), items, `flex-direction`, `justify-content`, `align-items`, `flex-wrap`.
            *   CSS Grid: Container (`display: grid`), `grid-template-columns`, `grid-template-rows`, `grid-gap`, item placement.
        *   Specificity: How browsers decide which CSS rules apply.
        *   Units: `px`, `em`, `rem`, `%`, `vw`, `vh`.
        *   Linking CSS: External (`<link>`), internal (`<style>`), inline (`style` attribute).

*   ### [Tailwind CSS](tailwind_css.md)
    *   Core Concept: Utility-first CSS framework.
    *   Setup: Installation (CDN, npm/yarn), configuration file (`tailwind.config.js`).
    *   Applying Classes: Directly in HTML elements.
    *   Layout:
        *   Containers: `container`.
        *   Display: `block`, `inline-block`, `inline`, `flex`, `grid`, `hidden`.
        *   Positioning: `static`, `fixed`, `absolute`, `relative`, `sticky`.
        *   Flexbox: `flex`, `flex-row`, `flex-col`, `items-center`, `justify-between`, `flex-grow`, `flex-shrink`.
        *   Grid: `grid`, `grid-cols-*`, `grid-rows-*`, `gap-*`, `col-span-*`.
    *   Styling:
        *   Sizing: `w-*` (width), `h-*` (height), `p-*` (padding), `m-*` (margin).
        *   Typography: `font-*`, `text-*` (size, color, alignment).
        *   Backgrounds: `bg-*` (color, image).
        *   Borders: `border`, `border-*` (color, width, style), `rounded-*`.
        *   Shadows: `shadow-*`.
    *   Responsiveness: Prefixes for breakpoints (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`). Example: `md:text-lg`.
    *   States: Prefixes for hover, focus, active, etc. (`hover:bg-blue-700`, `focus:ring`).
    *   Customization: Modifying `tailwind.config.js` (theme, variants, plugins).
    *   Directives: `@tailwind`, `@apply`, `@layer`.

*   ### [React](react.md)
    *   Core Concepts: Components, JSX, Virtual DOM.
    *   Setup: Create React App, Vite.
    *   JSX: Syntax, embedding expressions (`{}`), attributes, children.
    *   Components:
        *   Functional Components: Simple functions returning JSX.
        *   Class Components (less common now): `extends React.Component`, `render()` method.
    *   Props (Properties): Passing data from parent to child components, `props` object, `props.children`.
    *   State: Managing component-specific data that can change over time.
        *   `useState` Hook: For functional components (`const [value, setValue] = useState(initialValue)`).
        *   `this.state` and `this.setState` (for class components).
    *   Lifecycle (Functional Components with Hooks):
        *   `useEffect`: For side effects (data fetching, subscriptions, manually changing DOM). Dependencies array. Cleanup function.
    *   Handling Events: `onClick`, `onChange`, etc., event handlers.
    *   Conditional Rendering: `if` statements, ternary operator (`{condition ? <True /> : <False />}`), logical `&&` operator.
    *   Lists and Keys: Rendering collections of items, `map()` function, `key` prop for list items.
    *   Forms: Controlled components, handling form input and submission.
    *   Hooks (Common):
        *   `useState`: Manage state.
        *   `useEffect`: Handle side effects.
        *   `useContext`: Access context API.
        *   `useReducer`: For complex state logic.
        *   `useCallback`, `useMemo`: Performance optimizations.
    *   Component Patterns: Container/Presentational, Higher-Order Components (HOCs), Render Props (less common with hooks).
    *   Context API: For global state management or avoiding prop drilling.
    *   Routing: (e.g., React Router) `BrowserRouter`, `Route`, `Link`, `Switch` (or `Routes` in v6).

*   ### [Vue.js](vuejs.md)
    *   Core Concepts: Progressive framework, components, template syntax, reactivity.
    *   Setup: CDN, Vue CLI, Vite.
    *   Vue Instance / Application: `createApp()`.
    *   Template Syntax:
        *   Text Interpolation: `{{ message }}`.
        *   Raw HTML: `v-html`.
        *   Attribute Bindings: `v-bind:id` or `:id`.
        *   JavaScript Expressions: Inside `{{ }}` and `v-bind`.
    *   Directives: `v-if`, `v-else`, `v-else-if`, `v-show`, `v-for`, `v-on:click` or `@click`, `v-model`, `v-bind`, `v-slot`.
    *   Reactivity: Data properties in `data()` option.
    *   Computed Properties: `computed` option, cached based on reactive dependencies.
    *   Watchers: `watch` option, perform actions in response to data changes.
    *   Class and Style Bindings: `:class`, `:style`.
    *   Event Handling: `@click`, `@submit`, event modifiers (`.prevent`, `.stop`).
    *   Forms: `v-model` for two-way data binding on form inputs.
    *   Components:
        *   Definition: Single File Components (`.vue` files: `<template>`, `<script>`, `<style>`).
        *   Props: Declaring and passing data to child components.
        *   Emitting Events: `$emit` from child to parent.
        *   Slots: For content distribution.
    *   Lifecycle Hooks: `created`, `mounted`, `updated`, `unmounted`, etc. (Options API vs Composition API).
    *   Composition API (Vue 3+): `setup()` function, `ref`, `reactive`, `computed`, `watch`, lifecycle hooks (e.g., `onMounted`).
    *   Routing (Vue Router): `createRouter`, `routes` configuration, `<router-link>`, `<router-view>`.
    *   State Management (Pinia / Vuex): For larger applications.

**📦 DevOps & Deployment**

*   ### [Kubernetes](kubernetes.md)
    *   Core Concepts: Clusters, Nodes (Master/Control Plane, Worker), Containers.
    *   Key Objects:
        *   Pods: Smallest deployable unit, one or more containers, shared storage/network.
        *   Services: Abstract way to expose an application running on a set of Pods (e.g., ClusterIP, NodePort, LoadBalancer).
        *   Deployments: Declarative updates for Pods and ReplicaSets, manages stateless applications.
        *   ReplicaSets: Ensures a specified number of Pod replicas are running.
        *   Namespaces: Virtual clusters within a physical cluster.
        *   ConfigMaps & Secrets: Externalized configuration and sensitive data.
        *   Volumes: Persistent storage for Pods.
        *   Ingress: Manages external access to services, typically HTTP.
    *   `kubectl` Commands (Common):
        *   Cluster Info: `kubectl cluster-info`, `kubectl get nodes`.
        *   Managing Objects:
            *   `kubectl get <object-type> [object-name] [-n namespace] [-o wide/yaml/json]` (e.g., `kubectl get pods`)
            *   `kubectl describe <object-type> <object-name>`
            *   `kubectl apply -f <filename.yaml>`
            *   `kubectl delete -f <filename.yaml>` or `kubectl delete <object-type> <object-name>`
            *   `kubectl create <object-type> ...` (imperative, less common for deployments)
        *   Interacting with Pods:
            *   `kubectl logs <pod-name> [-c container-name]`
            *   `kubectl exec -it <pod-name> -- /bin/bash` (or other command)
            *   `kubectl port-forward <pod-name> <local-port>:<pod-port>`
        *   Scaling: `kubectl scale deployment <deployment-name> --replicas=<count>`
        *   Rollouts: `kubectl rollout status deployment/<name>`, `kubectl rollout history deployment/<name>`, `kubectl rollout undo deployment/<name>`.
    *   Manifest Files (YAML): Defining Kubernetes objects declaratively.

*   ### [CI/CD (GitHub Actions)](cicd_github_actions.md)
    *   Core Concepts: Automation of build, test, and deployment pipelines.
    *   Workflow Syntax (YAML files in `.github/workflows/`):
        *   `name`: Workflow name displayed on GitHub.
        *   `on`: Triggers for the workflow.
            *   Events: `push`, `pull_request`, `schedule`, `workflow_dispatch`.
            *   Filters: `branches`, `tags`, `paths`.
        *   `jobs`: Contains one or more jobs that run in parallel by default (can be sequential).
            *   `<job_id>`: Unique identifier for the job.
            *   `runs-on`: Type of runner (e.g., `ubuntu-latest`, `windows-latest`, `macos-latest`, self-hosted).
            *   `steps`: Sequence of tasks within a job.
                *   `name`: Name of the step.
                *   `uses`: Action to use (e.g., `actions/checkout@v3`, `actions/setup-node@v3`).
                *   `run`: Command-line programs to execute.
                *   `with`: Input parameters for an action.
                *   `env`: Environment variables for the step.
        *   `env`: Environment variables for the entire workflow or specific jobs.
    *   Actions: Reusable units of code (e.g., checking out code, setting up Node.js, building Docker images).
    *   Triggers:
        *   Push to a branch: `on: push: branches: [ main ]`
        *   Pull request to a branch: `on: pull_request: branches: [ main ]`
        *   Scheduled run: `on: schedule: - cron: '0 * * * *'` (hourly)
        *   Manual trigger: `on: workflow_dispatch`
    *   Jobs:
        *   Dependencies: `needs: <job_id>` to run jobs sequentially.
        *   Strategy Matrix: `strategy: matrix: node-version: [16, 18, 20]` to run a job multiple times with different configurations.
    *   Secrets: Storing sensitive data (`secrets.GITHUB_TOKEN`, custom secrets).
    *   Artifacts: Storing files produced by a job (`actions/upload-artifact`, `actions/download-artifact`).
    *   Example Workflow Snippet (Build and Test Node.js app):
        ```yaml
        name: Node.js CI
        on: [push, pull_request]
        jobs:
          build:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@v3
            - name: Use Node.js
              uses: actions/setup-node@v3
              with:
                node-version: '18'
            - run: npm ci
            - run: npm run build --if-present
            - run: npm test
        ```

*   ### [Ansible](ansible.md)
    *   Core Concepts: Agentless automation, idempotent, declarative language (YAML).
    *   Components:
        *   Control Node: Machine where Ansible is installed and run.
        *   Managed Nodes (Hosts): Servers being managed.
        *   Inventory: File (INI or YAML) defining managed nodes, groups, and variables.
        *   Playbooks: YAML files defining a set of plays to run.
        *   Plays: A set of tasks run against a group of hosts.
        *   Tasks: Units of action, typically calling a module.
        *   Modules: Reusable scripts that perform specific actions (e.g., `apt`, `yum`, `copy`, `service`, `user`).
        *   Roles: Way to organize playbooks into reusable structures.
        *   Handlers: Tasks triggered by `notify` directives, typically run at the end of a play.
        *   Variables: Used for customization (defined in inventory, playbooks, roles, etc.).
    *   Inventory File (`inventory.ini` or `inventory.yml`):
        *   Example (INI):
            ```ini
            [webservers]
            web1.example.com
            web2.example.com ansible_user=ubuntu
            [dbservers]
            db1.example.com
            ```
    *   Playbook Structure (YAML):
        ```yaml
        ---
        - name: Configure web servers
          hosts: webservers
          become: yes # Equivalent to sudo
          tasks:
            - name: Install nginx
              ansible.builtin.apt: # or yum for RHEL-based
                name: nginx
                state: present
            - name: Ensure nginx is running and enabled
              ansible.builtin.service:
                name: nginx
                state: started
                enabled: yes
            - name: Copy nginx config
              ansible.builtin.copy:
                src: files/nginx.conf
                dest: /etc/nginx/nginx.conf
              notify: Restart nginx
          handlers:
            - name: Restart nginx
              ansible.builtin.service:
                name: nginx
                state: restarted
        ```
    *   Common Modules:
        *   Package Management: `apt`, `yum`, `dnf`, `pacman`, `pip`.
        *   File Management: `copy`, `template`, `file`, `lineinfile`, `blockinfile`, `fetch`.
        *   Service Management: `service`, `systemd`.
        *   User Management: `user`, `group`.
        *   Command Execution: `command`, `shell`, `script`.
        *   Source Control: `git`.
    *   Running Playbooks: `ansible-playbook -i <inventory_file> <playbook.yml>`.
    *   Ad-hoc Commands: `ansible <host-pattern> -m <module> -a "<args>"`.
    *   Ansible Vault: Encrypting sensitive data.

*   ### [Docker](docker.md)
*   ### [OpenShift](openshift.md)
*   ### [Podman](podman.md)

**🗃️ Database & Data Handling**

*   ### [PostgreSQL](postgresql.md)
    *   Basic `psql` commands: `\l` (list DBs), `\c dbname` (connect), `\dt` (list tables), `\d table` (describe table), `\q` (quit).
    *   Data Types (Common):
        *   Numeric: `INTEGER`, `BIGINT`, `SMALLINT`, `NUMERIC(precision, scale)`, `REAL`, `DOUBLE PRECISION`, `SERIAL` (auto-incrementing int).
        *   Character: `VARCHAR(n)`, `CHAR(n)`, `TEXT`.
        *   Date/Time: `DATE`, `TIME`, `TIMESTAMP` (with/without time zone), `INTERVAL`.
        *   Boolean: `BOOLEAN`.
        *   JSON: `JSON`, `JSONB` (binary, more efficient, supports indexing).
        *   Array: `datatype[]` (e.g., `INTEGER[]`).
    *   Common Queries (SQL):
        *   `SELECT column1, column2 FROM table_name WHERE condition ORDER BY column LIMIT count OFFSET skip;`
        *   `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`
        *   `UPDATE table_name SET column1 = value1 WHERE condition;`
        *   `DELETE FROM table_name WHERE condition;`
        *   `CREATE TABLE table_name (column_name DATATYPE constraints, ...);` (Constraints: `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `DEFAULT`, `CHECK`).
        *   `ALTER TABLE table_name ADD COLUMN ...`, `DROP COLUMN ...`, `ALTER COLUMN ... TYPE ...`.
        *   `DROP TABLE table_name;`
    *   Joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`.
    *   Aggregate Functions: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `GROUP BY`.
    *   Indexes: `CREATE INDEX index_name ON table_name (column_name);` (Types: B-tree, Hash, GiST, GIN). Improves query performance.
    *   Transactions: `BEGIN; ... COMMIT;` or `ROLLBACK;`.
    *   Views: `CREATE VIEW view_name AS SELECT ...;`.

*   ### [MySQL](mysql.md)
    *   Basic `mysql` client commands: `SHOW DATABASES;`, `USE database_name;`, `SHOW TABLES;`, `DESCRIBE table_name;`, `EXIT;`.
    *   Data Types (Common):
        *   Numeric: `INT`, `BIGINT`, `SMALLINT`, `TINYINT`, `DECIMAL(M,D)`, `FLOAT`, `DOUBLE`. `AUTO_INCREMENT` for primary keys.
        *   String: `VARCHAR(N)`, `CHAR(N)`, `TEXT`, `BLOB`.
        *   Date/Time: `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` (auto-updates by default).
        *   Boolean: `BOOL` or `BOOLEAN` (alias for `TINYINT(1)`).
        *   Enum: `ENUM('val1', 'val2', ...)`.
        *   JSON (MySQL 5.7+).
    *   SQL Queries (largely same as PostgreSQL, minor syntax differences):
        *   `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`.
    *   Joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`. (MySQL doesn't have `FULL OUTER JOIN` directly, emulated with `UNION`).
    *   Subqueries: Queries nested inside another query (in `SELECT`, `FROM`, `WHERE`, `HAVING`).
    *   Aggregate Functions: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, used with `GROUP BY`.
    *   Indexes: `CREATE INDEX index_name ON table_name (column_name);`. `PRIMARY KEY`, `UNIQUE INDEX`, `FULLTEXT INDEX`.
    *   Storage Engines: InnoDB (default, ACID, row-level locking, foreign keys), MyISAM (older, table-level locking).
    *   Optimization Tips: Use appropriate data types, index columns used in `WHERE`/`JOIN`/`ORDER BY`, `EXPLAIN` query to analyze execution plan.
    *   User Management: `CREATE USER`, `GRANT PRIVILEGES`, `REVOKE PRIVILEGES`.

*   ### [SQLite](sqlite.md)
    *   Characteristics: Serverless, self-contained, zero-configuration, transactional SQL database engine. Database is a single file.
    *   `sqlite3` CLI: `.open filename.db`, `.tables`, `.schema tablename`, `.quit`, `.help`.
    *   Data Types (Dynamic Typing - more flexible, called "Type Affinity"): `NULL`, `INTEGER`, `REAL`, `TEXT`, `BLOB`.
    *   SQL Syntax: Largely standard SQL.
        *   `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`.
        *   `PRIMARY KEY AUTOINCREMENT` for auto-incrementing integer keys.
    *   Lite Queries: Suitable for embedded applications, local data storage, caching.
    *   Transactions: `BEGIN TRANSACTION; ... COMMIT;` or `ROLLBACK;`. (Atomic by default for single statements).
    *   Indexes: `CREATE INDEX index_name ON table_name (column_name);`.
    *   Pragmas: Special commands to modify SQLite operation or query internal data (e.g., `PRAGMA foreign_keys = ON;`).
    *   Storage: Single file on disk.
    *   Use Cases: Mobile apps, desktop apps, small websites, data analysis for small datasets.
    *   Limitations: Limited concurrency (writer locks the entire database), no user management, fewer built-in functions compared to server-based RDBMS.

*   ### [Regex](regex.md)
    *   Purpose: Pattern matching in text.
    *   Basic Metacharacters:
        *   `.`: Any single character (except newline).
        *   `^`: Start of string/line.
        *   `$`: End of string/line.
        *   `*`: Zero or more of the preceding character/group.
        *   `+`: One or more of the preceding character/group.
        *   `?`: Zero or one of the preceding character/group (also for non-greedy matching).
        *   `\`: Escape character (e.g., `\.` matches a literal dot).
    *   Character Classes:
        *   `[abc]`: Matches 'a', 'b', or 'c'.
        *   `[^abc]`: Matches any character except 'a', 'b', or 'c'.
        *   `[a-z]`: Matches any lowercase letter.
        *   `[0-9]`: Matches any digit.
        *   Predefined: `\d` (digit), `\D` (non-digit), `\s` (whitespace), `\S` (non-whitespace), `\w` (word char: alphanumeric + `_`), `\W` (non-word char).
    *   Quantifiers:
        *   `{n}`: Exactly n times.
        *   `{n,}`: At least n times.
        *   `{n,m}`: Between n and m times.
        *   Greedy vs. Non-greedy (Lazy): `*?`, `+?`, `??`, `{n,}?`.
    *   Groups and Capturing:
        *   `(pattern)`: Captures the matched substring.
        *   `(?:pattern)`: Non-capturing group.
        *   Backreferences: `\1`, `\2` refer to captured groups.
    *   Alternation: `|` (OR operator, e.g., `cat|dog`).
    *   Anchors and Boundaries: `\b` (word boundary), `\B` (non-word boundary).
    *   Lookahead/Lookbehind (Assertions):
        *   Positive Lookahead: `(?=pattern)`
        *   Negative Lookahead: `(?!pattern)`
        *   Positive Lookbehind: `(?<=pattern)`
        *   Negative Lookbehind: `(?<!pattern)`
    *   Flags/Modifiers (depend on implementation, e.g., in Python `re` module):
        *   `i`: Case-insensitive.
        *   `g`: Global match (in tools like `sed`, JavaScript).
        *   `m`: Multiline (`^` and `$` match start/end of lines).
    *   Common Expressions:
        *   Email: (complex, many variations, simple example: `^\S+@\S+\.\S+$`)
        *   URL: (complex, simple example: `^(https?|ftp)://[^\s/$.?#].[^\s]*$`)
        *   IP Address: `^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$`
        *   Date (YYYY-MM-DD): `^\d{4}-\d{2}-\d{2}$`

*   ### [JSON/YAML](json_yaml.md)
    *   **JSON (JavaScript Object Notation):**
        *   Syntax:
            *   Objects: `{ "key": "value", "number": 123, "nested": { ... } }` (Keys are strings).
            *   Arrays: `[ "apple", "banana", 100, { "object_in_array": true } ]`.
            *   Values: Strings (double-quoted), numbers, booleans (`true`, `false`), arrays, objects, `null`.
        *   Data Types: String, Number, Boolean, Array, Object, Null.
        *   Usage: Data interchange format, configuration files, APIs.
        *   Transformation Examples:
            *   Parsing (string to object): `JSON.parse()` (JavaScript), `json.loads()` (Python).
            *   Stringifying (object to string): `JSON.stringify()` (JavaScript), `json.dumps()` (Python).
    *   **YAML (YAML Ain't Markup Language):**
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

*   ### [SQL](sql.md)

**🔐 Security & Networking**

*   ### [SSH](ssh.md)
    *   Purpose: Secure remote login, command execution, file transfer.
    *   Key Concepts: Client-server model, encryption.
    *   Authentication Methods:
        *   Password-based (less secure, often disabled).
        *   Public Key Authentication (more secure, recommended):
            *   Generate key pair: `ssh-keygen -t rsa -b 4096` (or `ed25519`). Creates `id_rsa` (private) and `id_rsa.pub` (public).
            *   Copy public key to server: `ssh-copy-id user@host` or manually add to `~/.ssh/authorized_keys` on server.
    *   Connecting: `ssh user@hostname -p port_number` (default port is 22).
    *   Configuration File (`~/.ssh/config` on client):
        ```
        Host myserver
            HostName server.example.com
            User myuser
            Port 2222
            IdentityFile ~/.ssh/my_custom_key
        ```
    *   Tunneling (Port Forwarding):
        *   Local Port Forwarding: `ssh -L local_port:destination_host:destination_port user@ssh_server_host` (Access `destination_host:destination_port` via `localhost:local_port`).
        *   Remote Port Forwarding: `ssh -R remote_port:local_host:local_port user@ssh_server_host` (Access `local_host:local_port` on client via `ssh_server_host:remote_port`).
        *   Dynamic Port Forwarding (SOCKS proxy): `ssh -D local_port user@ssh_server_host`.
    *   File Transfer:
        *   `scp`: `scp source_file user@host:destination_path` or `scp user@host:source_file destination_path`.
        *   `sftp`: Interactive file transfer program.
    *   `sshd_config` (Server configuration, usually `/etc/ssh/sshd_config`): Hardening options (e.g., `PasswordAuthentication no`, `PermitRootLogin no`, `AllowUsers`).
    *   Agent Forwarding: `ssh -A user@host` (use with caution, allows remote host to use your local SSH keys).

*   ### [Firewall (UFW/iptables)](firewall_ufw_iptables.md)
    *   **UFW (Uncomplicated Firewall) - Frontend for iptables:**
        *   Purpose: Simplify firewall management on Linux.
        *   Status: `sudo ufw status` or `sudo ufw status verbose`.
        *   Enable/Disable: `sudo ufw enable`, `sudo ufw disable`.
        *   Default Policies:
            *   `sudo ufw default deny incoming`
            *   `sudo ufw default allow outgoing`
        *   Allowing Connections:
            *   By port: `sudo ufw allow 22` (for SSH) or `sudo ufw allow 22/tcp`.
            *   By service name: `sudo ufw allow ssh` (uses `/etc/services`).
            *   Specific IP: `sudo ufw allow from 192.168.1.100`.
            *   Specific IP and port: `sudo ufw allow from 192.168.1.100 to any port 22 proto tcp`.
        *   Denying Connections: `sudo ufw deny 80`.
        *   Deleting Rules: `sudo ufw delete allow 80` or by number `sudo ufw status numbered`, then `sudo ufw delete <number>`.
        *   Rate Limiting: `sudo ufw limit ssh`.
    *   **iptables - Low-level packet filtering:**
        *   Concepts: Tables (filter, nat, mangle, raw), Chains (INPUT, OUTPUT, FORWARD, PREROUTING, POSTROUTING), Rules, Targets (ACCEPT, DROP, REJECT, LOG).
        *   Listing Rules: `sudo iptables -L -v -n` (for filter table). `sudo iptables -t nat -L -v -n` (for NAT table).
        *   Flushing Rules: `sudo iptables -F` (flush all rules in filter table).
        *   Setting Default Policies:
            *   `sudo iptables -P INPUT DROP`
            *   `sudo iptables -P FORWARD DROP`
            *   `sudo iptables -P OUTPUT ACCEPT`
        *   Allowing Specific Traffic (Examples):
            *   Allow established connections: `sudo iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT`
            *   Allow loopback: `sudo iptables -A INPUT -i lo -j ACCEPT`
            *   Allow SSH: `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`
            *   Allow HTTP/HTTPS: `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT`, `sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT`
        *   Saving Rules: Varies by distro (e.g., `iptables-save > /etc/iptables/rules.v4` and `iptables-persistent` package on Debian/Ubuntu).
        *   Logging Dropped Packets: `sudo iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables_INPUT_denied: " --log-level 7` (then drop).

*   ### [SSL/TLS (Cert Generation, OpenSSL)](ssltls_openssl.md)
    *   Purpose: Secure communication over networks (e.g., HTTPS). Encryption, Authentication, Integrity.
    *   Key Concepts: Certificates (Public Key, Identity Info, Signature from CA), Certificate Authority (CA), Private Key, CSR (Certificate Signing Request).
    *   OpenSSL Commands:
        *   Generate Private Key: `openssl genpkey -algorithm RSA -out private_key.pem -aes256` (encrypted) or `openssl genpkey -algorithm RSA -out private_key.pem` (unencrypted). For EC: `openssl ecparam -name prime256v1 -genkey -noout -out private_key.pem`.
        *   Generate CSR: `openssl req -new -key private_key.pem -out certificate_request.csr` (prompts for details: CN, Org, etc.).
        *   Generate Self-Signed Certificate (for testing/internal use):
            `openssl req -x509 -newkey rsa:4096 -keyout private_key.pem -out certificate.pem -days 365 -nodes` (combines key and CSR generation).
        *   View Certificate Details: `openssl x509 -in certificate.pem -text -noout`.
        *   View CSR Details: `openssl req -in certificate_request.csr -text -noout`.
        *   Verify Certificate against CA: `openssl verify -CAfile ca_certificate.pem certificate.pem`.
        *   Convert Formats:
            *   PEM to DER: `openssl x509 -inform pem -in cert.pem -outform der -out cert.der`.
            *   PEM to PKCS#12 (.pfx, .p12 - bundles key and cert): `openssl pkcs12 -export -out certificate.pfx -inkey private_key.pem -in certificate.pem [-certfile CACert.pem]`.
        *   Test SSL/TLS Connection: `openssl s_client -connect example.com:443`.
    *   Certificate Types: Domain Validated (DV), Organization Validated (OV), Extended Validation (EV).
    *   Let's Encrypt / Certbot: Free, automated CA. `certbot certonly --standalone -d example.com` or `certbot --nginx -d example.com`.

*   ### [GPG Encryption](gpg_encryption.md)
    *   Purpose: Encryption and signing of data and communications. Based on OpenPGP standard.
    *   Key Management:
        *   Generate Key Pair: `gpg --full-generate-key` (choose key type, size, expiry, user ID).
        *   List Keys: `gpg --list-keys` (public), `gpg --list-secret-keys` (private).
        *   Export Public Key: `gpg --export -a "User Name or Email" > public_key.asc`.
        *   Import Public Key: `gpg --import public_key.asc`.
        *   Edit Key (trust, sign, etc.): `gpg --edit-key "User Name or Email"`.
        *   Delete Key: `gpg --delete-secret-keys "key_id"`, `gpg --delete-key "key_id"`.
    *   Encrypting Files:
        *   For a recipient (using their public key): `gpg --encrypt --recipient "Recipient Name or Email" -o encrypted_file.gpg original_file`.
        *   Symmetric Encryption (password-based): `gpg --symmetric -o encrypted_file.gpg original_file`.
    *   Decrypting Files: `gpg --decrypt encrypted_file.gpg -o decrypted_file` or `gpg -d encrypted_file.gpg > decrypted_file`. (Prompts for passphrase if private key is protected).
    *   Signing Files:
        *   Create a signature: `gpg --sign -o signed_document.gpg document` (creates a compressed signed file).
        *   Create a detached signature: `gpg --detach-sign -o document.sig document`.
        *   Clear-sign (for text files, human-readable): `gpg --clearsign document.txt`.
    *   Verifying Signatures:
        *   For `.gpg` signed file: `gpg --decrypt signed_document.gpg` (also verifies).
        *   For detached signature: `gpg --verify document.sig document`.
    *   Key Servers: Uploading/downloading public keys (`gpg --send-keys key_id`, `gpg --recv-keys key_id`).
    *   Agent (`gpg-agent`): Caches passphrases.

*   ### [nmap](nmap.md)
    *   Purpose: Network discovery and security auditing.
    *   Common Scan Types:
        *   Ping Scan (Host Discovery): `nmap -sn target_network` (e.g., `192.168.1.0/24`). No port scan.
        *   TCP SYN Scan (Default, Stealthy): `nmap -sS target_host`.
        *   TCP Connect Scan: `nmap -sT target_host` (full TCP handshake, more detectable).
        *   UDP Scan: `nmap -sU target_host` (slower, often combined with `-p` for specific ports).
        *   Version Detection: `nmap -sV target_host` (tries to determine service/version on open ports).
        *   OS Detection: `nmap -O target_host` (requires root/admin).
        *   Aggressive Scan: `nmap -A target_host` (enables OS detection, version detection, script scanning, and traceroute).
        *   Script Scanning (NSE - Nmap Scripting Engine): `nmap -sC target_host` (default scripts) or `nmap --script <script-name_or_category> target_host`.
    *   Target Specification: Single IP, hostname, network range (e.g., `192.168.1.1-100`, `192.168.1.0/24`), list from file (`-iL file.txt`).
    *   Port Specification:
        *   Default: Scans 1000 most common TCP ports.
        *   Specific ports: `-p 80,443,8080`.
        *   Port range: `-p 1-1024`.
        *   All ports: `-p-` (or `-p 1-65535`).
        *   Fast scan (fewer ports): `-F`.
    *   Timing and Performance:
        *   Timing templates: `-T0` (paranoid) to `-T5` (insane). Default is `-T3`. `-T4` is common for faster scans.
    *   Output Formats:
        *   Normal: Default console output.
        *   XML: `-oX output.xml`.
        *   Grepable: `-oG output.grep`.
        *   Script Kiddie: `-oS output.skriptkiddie`.
        *   All formats: `-oA basename`.
    *   Examples:
        *   Scan top ports on a host: `nmap target.example.com`
        *   Discover live hosts on a network: `nmap -sn 192.168.1.0/24`
        *   Scan specific TCP ports with version detection: `nmap -sV -p 22,80,443 target.example.com`
        *   Run default vulnerability scripts: `nmap --script vuln target.example.com`
    *   Ethical Use: Only scan networks/hosts you have explicit permission to scan.

*   ### [fail2ban](fail2ban.md)
    *   Purpose: Intrusion prevention software that monitors log files for malicious patterns and bans offending IPs using firewall rules.
    *   Configuration:
        *   Main config: `/etc/fail2ban/fail2ban.conf` (usually not modified directly).
        *   Local overrides: `/etc/fail2ban/fail2ban.local`.
        *   Jail config: `/etc/fail2ban/jail.conf` (contains default jails, not modified directly).
        *   Local jail overrides: `/etc/fail2ban/jail.local` (primary file for customization) or individual files in `/etc/fail2ban/jail.d/`.
    *   Jail Setup (`jail.local`):
        *   `[DEFAULT]` section: Global settings (e.g., `bantime`, `findtime`, `maxretry`).
        *   Specific Jails: `[sshd]`, `[apache-auth]`, etc.
            *   `enabled = true/false`: Activates or deactivates the jail.
            *   `port = ssh` (or port number).
            *   `filter = sshd` (name of the filter file in `/etc/fail2ban/filter.d/`).
            *   `logpath = /var/log/auth.log` (path to the log file to monitor).
            *   `maxretry = 5`: Number of failures before banning.
            *   `bantime = 1h` (1 hour), `1d` (1 day), `-1` (permanent).
            *   `findtime = 10m`: Time window in which `maxretry` must occur.
            *   `action = %(action_)s` (default action), `%(action_mw)s` (ban & mail), `%(action_mwl)s` (ban & mail with whois and logs).
    *   Filter Files (`/etc/fail2ban/filter.d/*.conf`): Contain regular expressions (`failregex`) to detect malicious attempts.
    *   Actions (`/etc/fail2ban/action.d/*.conf`): Define commands to execute when an IP is banned/unbanned (e.g., adding/removing iptables rules).
    *   Client (`fail2ban-client`):
        *   Status: `sudo fail2ban-client status`.
        *   Status of a specific jail: `sudo fail2ban-client status sshd`.
        *   Unban IP: `sudo fail2ban-client set sshd unbanip 1.2.3.4`.
        *   Reload configuration: `sudo fail2ban-client reload`.
    *   Example Jail for SSH:
        ```ini
        # In /etc/fail2ban/jail.local
        [sshd]
        enabled = true
        port = ssh
        filter = sshd
        logpath = /var/log/auth.log # For Debian/Ubuntu; /var/log/secure for CentOS/RHEL
        maxretry = 3
        bantime = 1d
        ```
    *   Testing Filters: `fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/sshd.conf`.

**👷 Platform-Specific**

*   ### [Capacitor](capacitor.md)
    *   Purpose: Cross-platform native runtime for web apps (alternative to Cordova). Allows web apps to run as native iOS, Android, and PWA.
    *   Core Concepts:
        *   Web View: Renders your web application.
        *   Native Bridge: Communication between web code and native code.
        *   Plugins: Access native device features (Camera, Geolocation, Filesystem, etc.).
    *   Setup:
        *   Install: `npm install @capacitor/core @capacitor/cli`.
        *   Initialize: `npx cap init [appName] [appId] --web-dir=www` (or your web app's build directory).
        *   Add Platforms: `npx cap add ios`, `npx cap add android`.
    *   Workflow:
        1.  Build your web app (e.g., `npm run build`).
        2.  Sync web assets to native platforms: `npx cap sync` (copies web dir, updates config).
        3.  Open native IDE: `npx cap open ios`, `npx cap open android`.
        4.  Build and run from native IDE (Xcode for iOS, Android Studio for Android).
    *   Plugins:
        *   Core Plugins: Bundled with Capacitor (e.g., `App`, `SplashScreen`, `StatusBar`, `Keyboard`, `Geolocation`).
        *   Community/Custom Plugins.
        *   Usage (JavaScript/TypeScript):
            ```typescript
            import { Camera, CameraResultType } from '@capacitor/camera';
            const takePicture = async () => {
              const image = await Camera.getPhoto({
                quality: 90,
                allowEditing: true,
                resultType: CameraResultType.Uri
              });
            };
            ```
    *   Configuration (`capacitor.config.json` or `.ts`): App ID, app name, web directory, plugin preferences.
    *   Native API Access: Use plugins or create custom native code.
    *   Deployment: Build native binaries through Xcode (IPA for iOS) and Android Studio (APK/AAB for Android). PWAs are deployed like any web app.
    *   Updating: `npx cap update` (updates native dependencies).

*   ### [PeopleSoft Integration Broker](peoplesoft_ib.md)
    *   Purpose: PeopleSoft's framework for synchronous and asynchronous messaging between PeopleSoft systems and third-party applications.
    *   Key Components:
        *   Gateway: Acts as the entry point for messages (listens for HTTP/S, JMS, etc.). Connects to Application Server(s).
        *   Application Server Domains: Handle message processing (routing, transformation, execution of PeopleCode).
        *   Messages: Data structures defining the payload (Rowset-based, Non-Rowset/XML, Document).
        *   Service Operations (formerly known as Message Definitions in older versions): Defines the transaction (e.g., request/response, one-way). Includes:
            *   Message: The data structure.
            *   Handlers: PeopleCode programs that process the message (OnRequest, OnResponse, OnError, etc.).
            *   Routings: Define the direction of the message (inbound/outbound) and transformation rules.
        *   Nodes: Represent PeopleSoft systems or external systems involved in integration. Contain connection information.
        *   Queues: For asynchronous messaging, ensures ordered and guaranteed delivery.
        *   Connectors: Adapters for different protocols (HTTP, JMS, FTP, File, etc.).
    *   Handlers (PeopleCode):
        *   Application Classes or Functions implementing specific interfaces (e.g., `PS_PT:Integration:IRequestHandler`).
        *   `OnRequest`: Processes incoming synchronous requests.
        *   `OnNotify`: Processes incoming asynchronous messages.
        *   `Transform` programs (XSLT or PeopleCode) for data mapping.
    *   Service Configuration: Done through PIA (PeopleSoft Internet Architecture) navigation: PeopleTools > Integration Broker > ...
    *   Monitoring: Integration Broker Monitor provides tools to view message status, errors, and logs.
    *   Common Use Cases: Exposing PeopleSoft components as web services (REST/SOAP), consuming external web services, EIPs (Enterprise Integration Patterns).
    *   Security: WS-Security for web services, node authentication, SSL/TLS.

*   ### [Azure CLI](azure_cli.md)
    *   Purpose: Command-line interface for managing Azure resources.
    *   Installation: Available for Windows, macOS, Linux.
    *   Login: `az login` (interactive) or `az login --service-principal -u APP_ID -p PASSWORD --tenant TENANT_ID`.
    *   Core Syntax: `az <group> <subgroup> <command> --parameters`.
    *   Common Groups and Commands:
        *   Account Management: `az account set --subscription <id>`, `az account list`.
        *   Resource Groups: `az group create --name MyResourceGroup --location eastus`, `az group list`, `az group delete`.
        *   Virtual Machines (VMs):
            *   `az vm create --resource-group MyRG --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys`
            *   `az vm list`, `az vm show`, `az vm start`, `az vm stop`, `az vm deallocate`, `az vm delete`.
        *   Storage:
            *   `az storage account create --name mystorageaccount --resource-group MyRG --location eastus --sku Standard_LRS`
            *   `az storage blob upload --account-name mystorageaccount --container-name mycontainer --name myfile.txt --file myfile.txt`
        *   App Service (Web Apps):
            *   `az appservice plan create --name MyPlan --resource-group MyRG --sku B1`
            *   `az webapp create --resource-group MyRG --plan MyPlan --name MyUniqueWebAppName --runtime "NODE|16-LTS"`
        *   Azure Kubernetes Service (AKS):
            *   `az aks create --resource-group MyRG --name MyAKSCluster --node-count 1 --generate-ssh-keys`
            *   `az aks get-credentials --resource-group MyRG --name MyAKSCluster`
        *   Azure SQL Database: `az sql server create`, `az sql db create`.
        *   Networking (VNet, Subnet, NSG): `az network vnet create`, `az network nsg create`.
    *   Parameters: `--name`, `--resource-group`, `--location`, `--sku`, specific options for each command.
    *   Output Formats: `--output json` (default), `table`, `tsv`, `yaml`.
    *   Querying Output: `--query` (uses JMESPath query language, e.g., `az vm list --query "[?location=='eastus'].name"`).
    *   Scripting: Use in Bash, PowerShell, or other scripting languages.
    *   Authentication: Interactive, service principal, managed identity.

*   ### [Google Cloud CLI (gcloud)](gcloud_cli.md)
    *   Purpose: Command-line interface for managing Google Cloud Platform (GCP) resources.
    *   Installation: Google Cloud SDK.
    *   Initialization & Authentication: `gcloud init` (sets up project, account, default region/zone), `gcloud auth login`.
    *   Core Syntax: `gcloud <component> <group> <command> --flags`.
    *   Common Components and Commands:
        *   Configuration: `gcloud config set project <project_id>`, `gcloud config set compute/zone <zone>`, `gcloud config list`.
        *   Compute Engine (VMs):
            *   `gcloud compute instances create my-vm --machine-type e2-medium --image-family debian-11 --image-project debian-cloud --zone us-central1-a`
            *   `gcloud compute instances list`, `gcloud compute instances describe my-vm`, `gcloud compute instances start/stop/delete my-vm`.
            *   `gcloud compute ssh my-vm`.
        *   Cloud Storage (Buckets & Objects):
            *   `gsutil mb gs://my-bucket` (gsutil is part of gcloud SDK for storage).
            *   `gsutil cp myfile.txt gs://my-bucket/`
            *   `gsutil ls gs://my-bucket/`
        *   Google Kubernetes Engine (GKE):
            *   `gcloud container clusters create my-cluster --num-nodes 3 --zone us-central1-a`
            *   `gcloud container clusters get-credentials my-cluster --zone us-central1-a` (configures kubectl).
        *   App Engine: `gcloud app deploy app.yaml`, `gcloud app browse`.
        *   Cloud SQL: `gcloud sql instances create my-instance --database-version MYSQL_8_0 --region us-central1`.
        *   Deployment Manager: `gcloud deployment-manager deployments create my-deployment --config my-config.yaml`.
    *   Flags: `--project`, `--zone`, `--region`, specific options for each command.
    *   Output Formats: `--format=json` (default is often YAML-like or text), `yaml`, `text`, `csv`, `table`.
    *   Filtering and Formatting Output: `--filter` (expression), `--format="value(name)"`.
    *   Scripting: Use in shell scripts.
    *   Service Accounts: For non-interactive authentication.

*   ### [Ionic](ionic.md)

**🛠️ Productivity & Utilities**

*   ### [Vim](vim.md)
    *   Modal Editor: Normal mode, Insert mode, Visual mode, Command-line mode.
    *   Basic Navigation (Normal Mode):
        *   `h` (left), `j` (down), `k` (up), `l` (right).
        *   `w` (next word), `b` (previous word), `e` (end of word).
        *   `0` (start of line), `^` (first non-blank char), `$` (end of line).
        *   `gg` (start of file), `G` (end of file), `:<line_number>` or `<line_number>G` (go to line).
        *   `Ctrl+f` (page down), `Ctrl+b` (page up).
    *   Editing (Normal Mode to Insert Mode):
        *   `i` (insert before cursor), `I` (insert at start of line).
        *   `a` (append after cursor), `A` (append at end of line).
        *   `o` (open new line below), `O` (open new line above).
    *   Editing (Normal Mode - Deletion, Change, Yank/Copy):
        *   `x` (delete character under cursor).
        *   `dd` (delete current line).
        *   `dw` (delete word).
        *   `d$` or `D` (delete to end of line).
        *   `cc` (change current line), `cw` (change word).
        *   `yy` or `Y` (yank/copy current line), `yw` (yank word).
        *   `p` (paste after cursor), `P` (paste before cursor).
        *   `u` (undo), `Ctrl+r` (redo).
    *   Visual Mode (`v` char-wise, `V` line-wise, `Ctrl+v` block-wise): Select text, then apply commands (e.g., `d`, `y`).
    *   Command-Line Mode (`:`):
        *   Saving: `:w` (write), `:wq` or `:x` or `ZZ` (write and quit).
        *   Quitting: `:q` (quit), `:q!` (quit without saving).
        *   Search: `/<pattern>`, `?<pattern>`. `n` (next), `N` (previous).
        *   Replace: `:%s/old/new/g` (replace all in file), `:%s/old/new/gc` (confirm replace).
        *   Set options: `:set number`, `:set paste`.
    *   `.vimrc`: Configuration file for Vim.

*   ### [VSCode](vscode.md)
    *   Command Palette: `Ctrl+Shift+P` or `Cmd+Shift+P`. Access all commands.
    *   Basic Editing: Standard text editing shortcuts.
    *   Navigation:
        *   Go to File: `Ctrl+P` or `Cmd+P`.
        *   Go to Symbol: `Ctrl+Shift+O` or `Cmd+Shift+O`.
        *   Go to Definition: `F12`.
        *   Find: `Ctrl+F` or `Cmd+F`. Find in Files: `Ctrl+Shift+F` or `Cmd+Shift+F`.
    *   Integrated Terminal: `Ctrl+\`` or `Cmd+\``.
    *   Source Control (Git): Built-in Git integration.
    *   Extensions: `Ctrl+Shift+X` or `Cmd+Shift+X`. Marketplace for language support, linters, themes, debuggers, etc.
        *   Popular: Prettier, ESLint, Python, Live Server, Docker, Remote - SSH.
    *   Debugging: `F5` to start, breakpoints, watch variables.
    *   Multi-cursor Editing: `Alt+Click` or `Ctrl+Alt+Down/Up` (`Cmd+Option+Down/Up`).
    *   Settings: `Ctrl+,` or `Cmd+,` (UI and JSON editor `settings.json`).
    *   Keyboard Shortcuts: Customizable (`Ctrl+K Ctrl+S` or `Cmd+K Cmd+S`).
    *   Snippets: User-defined code snippets.
    *   Tasks: Configure and run build tasks, scripts (`tasks.json`).

*   ### [Markdown](markdown.md)
    *   Purpose: Lightweight markup language with plain text formatting syntax.
    *   Syntax:
        *   Headings: `# H1`, `## H2`, `### H3`, etc.
        *   Paragraphs: Just text, separated by blank lines.
        *   Line Breaks: End a line with two or more spaces, then Return.
        *   Emphasis: `*italic*` or `_italic_`, `**bold**` or `__bold__`, `***bold italic***` or `___bold italic___`.
        *   Strikethrough: `~~strikethrough~~`.
        *   Lists:
            *   Unordered: `* item`, `- item`, or `+ item`.
            *   Ordered: `1. item`, `2. item`.
        *   Links: `[link text](url "optional title")`.
        *   Images: `![alt text](image_url "optional title")`.
        *   Code:
            *   Inline: `` `code` ``.
            *   Code Blocks: Indent by 4 spaces or use fenced code blocks:
                ```markdown
                ```language_name
                code block
                ```
                ```
        *   Blockquotes: `> This is a blockquote.`
        *   Horizontal Rule: `---`, `***`, or `___` on a line by themselves.
        *   Tables (Extended Markdown):
            ```markdown
            | Header 1 | Header 2 |
            |----------|----------|
            | Cell 1   | Cell 2   |
            | Cell 3   | Cell 4   |
            ```
        *   Escaping Characters: `\*` to display a literal asterisk.

*   ### [Curl & Wget](curl_wget.md)
    *   **curl (Client URL):**
        *   Purpose: Transfer data from or to a server, using various protocols (HTTP, HTTPS, FTP, etc.). Powerful for API testing.
        *   Basic GET: `curl http://example.com`.
        *   Output to File: `curl -o output.html http://example.com` or `curl -O http://example.com/file.tar.gz` (uses remote filename).
        *   Show Headers: `curl -I http://example.com` (HEAD request) or `curl -i http://example.com` (include response headers in output).
        *   Verbose Output: `curl -v http://example.com`.
        *   POST Request: `curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' http://example.com/api`.
        *   Other HTTP Methods: `-X PUT`, `-X DELETE`, etc.
        *   Sending Headers: `-H "Authorization: Bearer token"`.
        *   Following Redirects: `-L`.
        *   User Agent: `-A "My User Agent"`.
        *   Cookies: `-b "name=value"` (send), `-c cookie-jar.txt` (store received cookies).
        *   Insecure (ignore SSL errors, for testing): `-k`.
    *   **wget (World Wide Web Get):**
        *   Purpose: Non-interactive download of files from the web. Good for recursive downloads.
        *   Basic Download: `wget http://example.com/file.zip`.
        *   Output to Specific File: `wget -O output_filename.zip http://example.com/file.zip`.
        *   Recursive Download (e.g., mirror a site): `wget -r -np -k http://example.com` (`-r`: recursive, `-np`: no parent, `-k`: convert links). Use with caution.
        *   Limit Download Rate: `--limit-rate=100k`.
        *   Continue Interrupted Download: `-c`.
        *   Background Download: `-b`.
        *   Quiet Mode: `-q`.
        *   Specify User Agent: `--user-agent="My Agent"`.
        *   Ignore SSL errors: `--no-check-certificate`.

*   ### [tmux](tmux.md)
    *   Purpose: Manage multiple terminal sessions, windows, and panes within a single terminal window. Sessions persist even if you disconnect.
    *   Key Concepts:
        *   Server: Background process managing sessions.
        *   Session: A collection of windows.
        *   Window: A single screen, can be split into panes.
        *   Pane: A rectangular part of a window running a separate shell.
    *   Prefix Key: Default is `Ctrl+b`. Commands are issued by `Prefix` then `key`.
    *   Sessions:
        *   Start new session: `tmux new -s session_name`.
        *   List sessions: `tmux ls`.
        *   Attach to session: `tmux attach -t session_name` or `tmux a -t session_name`.
        *   Detach from session: `Prefix` `d`.
        *   Kill session: `tmux kill-session -t session_name`.
    *   Windows (within a session):
        *   Create new window: `Prefix` `c`.
        *   Next window: `Prefix` `n`.
        *   Previous window: `Prefix` `p`.
        *   Go to window by number: `Prefix` `0-9`.
        *   Rename window: `Prefix` `,`.
        *   Close window: `Prefix` `&`.
    *   Panes (within a window):
        *   Split horizontally: `Prefix` `%`.
        *   Split vertically: `Prefix` `"`.
        *   Navigate panes: `Prefix` `arrow_keys`.
        *   Close pane: `Prefix` `x` (or `exit` in shell).
        *   Zoom pane: `Prefix` `z` (toggle).
        *   Swap panes: `Prefix` `{` (previous), `Prefix` `}` (next).
        *   Resize panes: `Prefix` `Ctrl+arrow_keys` (hold Ctrl).
    *   Scrolling (Copy Mode): `Prefix` `[` then use arrow keys/PageUp/PageDown. `q` to exit copy mode.
    *   Configuration: `~/.tmux.conf`.

*   ### [Git](git.md)

### [CakePHP](cakephp.md)
<!-- Existing CakePHP link, kept it separate as it wasn't in the new categorization -->
