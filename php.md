# PHP Cheatsheet

This cheatsheet covers common PHP syntax, data types, operators, control structures, functions, arrays, string manipulation, superglobals, and basic Object-Oriented Programming (OOP).

## Basic Syntax

*   **PHP Tags**:
    ```php
    <?php
        // PHP code goes here
        echo "Hello, World!";
    ?>

    <?php echo "Short echo tag example"; ?> // If short_open_tag is enabled (not recommended for portability)
    <?= "Short echo tag (PHP 5.4+)"; ?> // Always available since PHP 5.4
    ```
*   **Comments**:
    ```php
    <?php
    // This is a single-line comment

    # This is also a single-line comment (less common)

    /*
    This is a
    multi-line comment.
    */
    ?>
    ```
*   **Outputting Data**:
    ```php
    <?php
    echo "Hello using echo. "; // No return value, can output multiple comma-separated strings
    echo "String1", " String2";

    print "Hello using print. "; // Returns 1, can only output one string
    // print "String1", "String2"; // Error

    $name = "Alice";
    printf("Hello, %s! You are %d years old.\n", $name, 30); // Formatted output

    $data = ['apple', 'banana'];
    var_dump($data); // Dumps information about a variable (type and value)
    print_r($data);  // Prints human-readable information about a variable
    ?>
    ```
*   **Variables**: Start with `$` followed by the variable name. Case-sensitive.
    ```php
    <?php
    $text = "This is a string";
    $number = 123;
    $float_num = 19.99;
    $is_active = true;
    $_myVariable = "Underscore prefix is valid";
    // $1variable = "Invalid"; // Cannot start with a number
    ?>
    ```
*   **Constants**: Use `define()` (older) or `const` (PHP 5.3+, preferred for class constants and global constants since PHP 5.6). Case-sensitive by default.
    ```php
    <?php
    define("SITE_URL", "https://www.example.com");
    echo SITE_URL;

    const MAX_USERS = 100; // Global constant (outside class)
    echo MAX_USERS;

    class MyClass {
        const APP_VERSION = "1.0"; // Class constant
    }
    echo MyClass::APP_VERSION;
    ?>
    ```

## Data Types

*   **Scalar Types**:
    *   `string`: Sequence of characters.
        ```php
        $name = "John Doe";
        $message = 'Welcome to PHP!';
        $multiline = "This is a\nmulti-line string.";
        $hereDoc = <<<EOT
        This is a heredoc string.
        It can span multiple lines.
        Variables are parsed: $name.
        EOT;
        $nowDoc = <<<'EOD'
        This is a nowdoc string.
        Variables are NOT parsed: $name.
        EOD;
        ```
    *   `integer` (or `int`): Whole numbers.
        ```php
        $age = 30;
        $negative = -10;
        $octal = 0123; // 83 in decimal
        $hex = 0x1A;   // 26 in decimal
        $binary = 0b1010; // 10 in decimal (PHP 5.4+)
        ```
    *   `float` (or `double`, `real`): Floating-point numbers.
        ```php
        $price = 19.99;
        $scientific = 1.2e3; // 1200
        ```
    *   `boolean` (or `bool`): `true` or `false` (case-insensitive for keywords, but `true`/`false` preferred).
        ```php
        $isLoggedIn = true;
        $hasPermission = false;
        ```
*   **Compound Types**:
    *   `array`: Ordered map (can be used as list, hash map, dictionary, etc.).
    *   `object`: Instance of a class.
    *   `callable`: Functions, methods, closures.
    *   `iterable` (PHP 7.1+): Can be `array` or an object implementing `Traversable`.
*   **Special Types**:
    *   `resource`: Special variable holding a reference to an external resource (e.g., file handle, database connection).
    *   `NULL` (or `null`): Represents a variable with no value (case-insensitive keyword, `null` preferred).
        ```php
        $var = null;
        ```

## Operators

*   **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulus), `**` (exponentiation - PHP 5.6+).
*   **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`, `.=` (string concatenation assignment).
*   **Comparison**:
    *   `==` (Equal, type juggling)
    *   `===` (Identical, same type and value) - **Preferred for strict comparison**
    *   `!=` or `<>` (Not equal, type juggling)
    *   `!==` (Not identical) - **Preferred**
    *   `<`, `>`, `<=`, `>=`
    *   `<=>` (Spaceship operator, PHP 7+): Returns -1, 0, or 1.
*   **Logical**:
    *   `&&` or `and` (Logical AND)
    *   `||` or `or` (Logical OR)
    *   `!` (Logical NOT)
    *   `xor` (Exclusive OR)
*   **String Concatenation**: `.` (dot operator)
    ```php
    $greeting = "Hello" . " " . "World!"; // "Hello World!"
    ```
*   **Error Control Operator**: `@` (suppresses error messages for an expression - use sparingly).
*   **Increment/Decrement**: `++$var`, `$var++`, `--$var`, `$var--`.
*   **Null Coalescing Operator (`??`) (PHP 7+)**:
    ```php
    $username = $_GET['user'] ?? 'guest'; // If $_GET['user'] is not set or null, use 'guest'
    ```
*   **Ternary Operator**: `(condition) ? value_if_true : value_if_false;`
    ```php
    $age = 20;
    $status = ($age >= 18) ? "adult" : "minor";
    ```

## Control Structures

*   **If/Elseif/Else**:
    ```php
    $score = 75;
    if ($score >= 90) {
        echo "Grade A";
    } elseif ($score >= 80) {
        echo "Grade B";
    } else {
        echo "Grade C or lower";
    }
    // Alternative syntax (less common, useful in templates):
    // if ($condition):
    //   // ...
    // elseif ($another_condition):
    //   // ...
    // else:
    //   // ...
    // endif;
    ```
*   **Switch**:
    ```php
    $day = "Mon";
    switch ($day) {
        case "Mon":
            echo "Start of the week.";
            break; // Important!
        case "Fri":
            echo "Almost weekend!";
            break;
        default:
            echo "Another day.";
    }
    ```
*   **Loops**:
    *   `for`:
        ```php
        for ($i = 0; $i < 5; $i++) {
            echo "Number: $i <br>";
        }
        ```
    *   `while`:
        ```php
        $count = 0;
        while ($count < 3) {
            echo "Count: $count <br>";
            $count++;
        }
        ```
    *   `do...while`: Executes at least once.
        ```php
        $k = 0;
        do {
            echo "k is: $k <br>";
            $k++;
        } while ($k < 3);
        ```
    *   `foreach`: For iterating over arrays and objects.
        ```php
        $colors = ["red", "green", "blue"];
        foreach ($colors as $color) {
            echo "$color <br>";
        }

        $person = ["name" => "Alice", "age" => 30];
        foreach ($person as $key => $value) {
            echo "$key: $value <br>";
        }
        ```
*   **Break and Continue**:
    *   `break;`: Exits the current loop (or switch). Can take an optional numeric argument to break out of multiple nested loops.
    *   `continue;`: Skips the current iteration and proceeds to the next. Can also take an optional numeric argument.
*   **`include`, `require`, `include_once`, `require_once`**: For including files.
    *   `include`: If file not found, issues a warning and script continues.
    *   `require`: If file not found, issues a fatal error and script stops.
    *   `_once` versions: Ensure the file is included only once.
    ```php
    // include 'header.php';
    // require_once 'config/database.php';
    ```

## Functions

*   **Defining Functions**:
    ```php
    function greet($name) {
        return "Hello, " . $name . "!";
    }
    echo greet("Bob"); // Output: Hello, Bob!
    ```
*   **Function Arguments**:
    *   Default argument values:
        ```php
        function welcome($name = "Guest") {
            echo "Welcome, $name!<br>";
        }
        welcome(); // Welcome, Guest!
        welcome("Charlie"); // Welcome, Charlie!
        ```
    *   Type Hinting (PHP 5+, more comprehensive in PHP 7+):
        ```php
        // PHP 7+ scalar type hints and return type declarations
        function add(int $a, int $b): int {
            return $a + $b;
        }
        // echo add(5, 3); // 8
        // echo add(5, "3 apples"); // TypeError in PHP 7 strict mode, or warning and coercion otherwise
        ```
    *   Variable-length argument lists (`...` splat operator, PHP 5.6+):
        ```php
        function sum(...$numbers) {
            $total = 0;
            foreach ($numbers as $num) {
                $total += $num;
            }
            return $total;
        }
        echo sum(1, 2, 3, 4); // 10
        ```
    *   Pass by reference (`&`):
        ```php
        function increment(&$value) {
            $value++;
        }
        $num = 5;
        increment($num);
        echo $num; // 6
        ```
*   **Anonymous Functions (Closures) (PHP 5.3+)**:
    ```php
    $sayHello = function($name) {
        echo "Hello $name from closure!<br>";
    };
    $sayHello("David");

    // Use with array_map, array_filter, etc.
    $numbers = [1, 2, 3, 4];
    $squared = array_map(function($n) { return $n * $n; }, $numbers);
    // print_r($squared);
    ```
*   **Arrow Functions (PHP 7.4+)**: Concise syntax for simple anonymous functions.
    ```php
    $numbers = [1, 2, 3, 4];
    $doubled = array_map(fn($n) => $n * 2, $numbers);
    // print_r($doubled);
    ```
*   **Variable Scope**: `global`, `local`, `static`.
    ```php
    $globalVar = "I am global";
    function testScope() {
        $localVar = "I am local";
        // echo $globalVar; // Error: undefined variable (unless using 'global' keyword)
        global $globalVar; // Make global variable accessible
        echo $globalVar . "<br>";

        static $staticVar = 0; // Persists between function calls
        $staticVar++;
        echo "Static var: $staticVar <br>";
    }
    testScope();
    testScope();
    ```

## Arrays

PHP arrays are very flexible.
*   **Indexed Arrays** (numeric keys, usually starting from 0):
    ```php
    $fruits = ["apple", "banana", "cherry"]; // Short syntax (PHP 5.4+)
    // $fruits = array("apple", "banana", "cherry"); // Older syntax
    echo $fruits[0]; // apple
    $fruits[] = "orange"; // Append
    ```
*   **Associative Arrays** (string keys):
    ```php
    $person = [
        "name" => "Alice",
        "age" => 30,
        "city" => "New York"
    ];
    echo $person["name"]; // Alice
    $person["email"] = "alice@example.com"; // Add new element
    ```
*   **Multi-dimensional Arrays**:
    ```php
    $students = [
        ["name" => "Bob", "grade" => "A"],
        ["name" => "Charlie", "grade" => "B"]
    ];
    echo $students[0]["name"]; // Bob
    ```
*   **Common Array Functions**:
    *   `count($array)`: Returns the number of elements.
    *   `is_array($var)`: Checks if a variable is an array.
    *   `in_array($needle, $haystack)`: Checks if a value exists in an array.
    *   `array_key_exists($key, $array)`: Checks if a key exists in an array.
    *   `array_keys($array)`: Returns all keys.
    *   `array_values($array)`: Returns all values.
    *   `array_push($array, $val1, $val2...)`: Pushes elements onto the end.
    *   `array_pop($array)`: Pops the element off the end.
    *   `array_shift($array)`: Shifts an element off the beginning.
    *   `array_unshift($array, $val1...)`: Prepends elements to the beginning.
    *   `array_merge($arr1, $arr2...)`: Merges arrays.
    *   `array_slice($array, $offset, $length = null, $preserve_keys = false)`: Extracts a slice.
    *   `sort($array)`, `rsort($array)`: Sort numerically/alphabetically (ascending/descending), re-indexes.
    *   `asort($array)`, `arsort($array)`: Sort associative arrays by values, preserving keys.
    *   `ksort($array)`, `krsort($array)`: Sort associative arrays by keys.
    *   `array_map($callback, $array1, ...)`: Applies a callback to elements of given arrays.
    *   `array_filter($array, $callback = null, $flag = 0)`: Filters elements using a callback.
    *   `array_reduce($array, $callback, $initial = null)`: Iteratively reduce array to a single value.
    *   `list($var1, $var2) = $array;`: Assigns array elements to variables (PHP < 7.1).
    *   `[$var1, $var2] = $array;`: Array destructuring (PHP 7.1+).
    ```php
    $numbers = [3, 1, 4];
    sort($numbers); // $numbers is now [1, 3, 4]
    // print_r($numbers);
    ```

## String Functions

PHP has a rich set of string manipulation functions.
*   `strlen($string)`: Get string length.
*   `strpos($haystack, $needle, $offset = 0)`: Find position of first occurrence of a substring (case-sensitive).
*   `stripos($haystack, $needle, $offset = 0)`: Case-insensitive `strpos`.
*   `substr($string, $start, $length = null)`: Return part of a string.
*   `str_replace($search, $replace, $subject, &$count = null)`: Replace all occurrences of search string with replacement.
*   `strtolower($string)`, `strtoupper($string)`: Convert to lowercase/uppercase.
*   `ucfirst($string)`, `ucwords($string)`: Uppercase first character / first character of each word.
*   `trim($string, $characters = " \t\n\r\0\x0B")`: Strip whitespace (or other characters) from beginning and end. `ltrim()`, `rtrim()`.
*   `explode($delimiter, $string, $limit = PHP_INT_MAX)`: Split a string by a delimiter into an array.
*   `implode($glue, $pieces)` or `join($glue, $pieces)`: Join array elements with a string.
*   `htmlspecialchars($string, $flags = ENT_COMPAT | ENT_HTML401, $encoding = 'UTF-8', $double_encode = true)`: Convert special characters to HTML entities (prevents XSS).
*   `nl2br($string, $is_xhtml = true)`: Inserts HTML line breaks before all newlines in a string.
*   `sprintf($format, ...$args)`: Return a formatted string.
*   `strcmp($str1, $str2)`, `strcasecmp($str1, $str2)`: Binary safe string comparison (case-sensitive/insensitive).

## Superglobals

Built-in variables that are always available in all scopes.
*   `$_GET`: Associative array of variables passed via URL parameters (query string).
    ```php
    // URL: page.php?name=John&age=25
    // $name = $_GET['name'] ?? 'Guest';
    // $age = $_GET['age'] ?? null;
    ```
*   `$_POST`: Associative array of variables passed via HTTP POST method (e.g., from forms).
    ```php
    // <form method="post" action="submit.php">
    //   <input type="text" name="username">
    //   <input type="submit">
    // </form>
    // In submit.php:
    // $username = $_POST['username'] ?? '';
    ```
*   `$_REQUEST`: Associative array containing contents of `$_GET`, `$_POST`, and `$_COOKIE`. (Order depends on `request_order` in `php.ini`).
*   `$_SERVER`: Array containing information such as headers, paths, and script locations.
    ```php
    // echo $_SERVER['SERVER_NAME']; // e.g., www.example.com
    // echo $_SERVER['REQUEST_METHOD']; // e.g., GET, POST
    // echo $_SERVER['PHP_SELF']; // Path to current script
    // echo $_SERVER['REMOTE_ADDR']; // IP address of the user
    ```
*   `$_SESSION`: Associative array containing session variables. Requires `session_start();`.
    ```php
    // session_start(); // Must be called before any output
    // $_SESSION['user_id'] = 123;
    // echo "User ID: " . ($_SESSION['user_id'] ?? 'Not set');
    // session_destroy(); // To end session
    ```
*   `$_COOKIE`: Associative array of variables passed via HTTP Cookies.
    ```php
    // setcookie("username", "JohnDoe", time() + (86400 * 30), "/"); // 86400 = 1 day
    // echo "Cookie username: " . ($_COOKIE['username'] ?? 'Not set');
    ```
*   `$_FILES`: Associative array of items uploaded via HTTP POST.
    ```php
    // <form method="post" enctype="multipart/form-data" action="upload.php">
    //   <input type="file" name="myFile">
    //   <input type="submit">
    // </form>
    // In upload.php:
    // if (isset($_FILES['myFile'])) {
    //    $fileName = $_FILES['myFile']['name'];
    //    $fileTmpName = $_FILES['myFile']['tmp_name'];
    //    $fileSize = $_FILES['myFile']['size'];
    //    $fileError = $_FILES['myFile']['error'];
    //    // move_uploaded_file($fileTmpName, "uploads/" . $fileName);
    // }
    ```
*   `$_ENV`: Associative array of environment variables.

## Object-Oriented Programming (OOP)

*   **Classes and Objects**:
    ```php
    class Car {
        // Properties (member variables)
        public $color = "red"; // public, protected, private
        public $model;
        private $engineStatus = "stopped"; // private

        // Constructor (PHP 5 method name, PHP 7+ __construct)
        public function __construct($model, $color = "blue") {
            $this->model = $model;
            $this->color = $color;
            echo "Car object for {$this->model} created.<br>";
        }

        // Methods
        public function startEngine() {
            $this->engineStatus = "running";
            echo "Engine started for {$this->model}.<br>";
        }

        public function getEngineStatus() {
            return $this->engineStatus;
        }

        // Destructor (called when object is no longer referenced or script ends)
        public function __destruct() {
            // echo "Car object for {$this->model} is being destroyed.<br>";
        }
    }

    $myCar = new Car("Toyota Camry", "Silver");
    $myCar->startEngine();
    echo "My car color: " . $myCar->color . "<br>";
    // echo $myCar->engineStatus; // Fatal error: Cannot access private property
    echo "Engine status: " . $myCar->getEngineStatus() . "<br>";
    ```
*   **Inheritance (`extends`)**:
    ```php
    class ElectricCar extends Car {
        public $batteryCapacity;

        public function __construct($model, $color, $capacity) {
            parent::__construct($model, $color); // Call parent constructor
            $this->batteryCapacity = $capacity;
        }

        // Override method
        public function startEngine() {
            echo "Electric motor started silently for {$this->model}.<br>";
            // parent::startEngine(); // Optionally call parent's method
        }

        public function chargeBattery() {
            echo "Charging battery for {$this->model} (Capacity: {$this->batteryCapacity} kWh).<br>";
        }
    }
    $tesla = new ElectricCar("Tesla Model S", "Black", 100);
    $tesla->startEngine();
    $tesla->chargeBattery();
    ```
*   **Access Modifiers**: `public`, `protected`, `private`.
*   **Static Properties and Methods (`static`)**: Belong to the class, not an instance. Accessed with `ClassName::`.
    ```php
    class MathUtils {
        public static $pi = 3.14159;
        public static function add($a, $b) {
            return $a + $b;
        }
    }
    echo MathUtils::$pi . "<br>";
    echo MathUtils::add(5, 10) . "<br>";
    ```
*   **Abstract Classes and Methods (`abstract`)**: Abstract class cannot be instantiated. Abstract method must be implemented by child class.
    ```php
    abstract class Shape {
        abstract public function getArea(): float;
        public function getDescription() { echo "This is a shape."; }
    }
    class Circle extends Shape {
        private $radius;
        public function __construct($radius) { $this->radius = $radius; }
        public function getArea(): float { return pi() * $this->radius * $this->radius; }
    }
    ```
*   **Interfaces (`interface`, `implements`)**: Define a contract for methods a class must implement.
    ```php
    interface Loggable {
        public function log($message);
    }
    class FileLogger implements Loggable {
        public function log($message) {
            file_put_contents("app.log", $message . "\n", FILE_APPEND);
        }
    }
    ```
*   **Traits (PHP 5.4+)**: Code reuse mechanism for single inheritance languages.
    ```php
    trait Sharable {
        public function share($item) {
            echo "Sharing " . $item . "<br>";
        }
    }
    class Post {
        use Sharable;
        public $title;
        public function __construct($title) { $this->title = $title; }
    }
    $myPost = new Post("My Awesome Post");
    $myPost->share($myPost->title); // Sharing My Awesome Post
    ```
*   **Namespaces (PHP 5.3+)**: Prevent naming collisions.
    ```php
    // file1.php
    // namespace App\Utilities;
    // class Logger { /* ... */ }

    // file2.php
    // namespace App\Services;
    // use App\Utilities\Logger; // Import
    // // use App\Utilities\Logger as FileLogger; // Alias
    // // $logger = new Logger();
    ```
*   **Magic Methods**: Methods with special names that PHP calls automatically in certain situations (e.g., `__construct`, `__destruct`, `__call`, `__get`, `__set`, `__toString`).

## Error Handling

*   **`try...catch...finally` (PHP 5+)**:
    ```php
    try {
        $divisor = 0;
        if ($divisor == 0) {
            throw new Exception("Division by zero error!");
        }
        $result = 10 / $divisor;
        echo $result;
    } catch (Exception $e) { // Catches Exception and its children
        echo "Caught exception: " . $e->getMessage() . "<br>";
    } finally {
        echo "This block always executes.<br>";
    }
    // PHP 7.1+ can catch multiple exceptions:
    // catch (DivisionByZeroError | ArithmeticError $e) { ... }
    ```
*   **Error Reporting**:
    ```php
    // error_reporting(E_ALL); // Report all errors
    // ini_set('display_errors', 1); // Display errors (for development)
    // ini_set('log_errors', 1); // Log errors
    // ini_set('error_log', '/path/to/php-error.log'); // Specify error log file
    ```


