# HTML & CSS Cheatsheet

This cheatsheet covers common HTML elements for structuring web pages and CSS selectors/properties for styling them, including layout techniques like Flexbox and CSS Grid.

## HTML (HyperText Markup Language) - Structure

HTML documents are made up of elements, which are represented by tags.

*   **Basic Document Structure**:
    ```html
    <!DOCTYPE html> <!-- Defines the document type to be HTML5 -->
    <html lang="en"> <!-- The root element, lang attribute for language -->
    <head>
        <meta charset="UTF-8"> <!-- Character set declaration -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- Responsive viewport settings -->
        <meta name="description" content="A brief description of the page">
        <title>Page Title</title> <!-- Title shown in browser tab or window title bar -->
        <link rel="stylesheet" href="style.css"> <!-- Link to external CSS file -->
        <!-- <link rel="icon" href="favicon.ico" type="image/x-icon"> -->
        <!-- <script src="script.js" defer></script> --> <!-- Link to JavaScript file (defer loads after HTML parsing) -->
    </head>
    <body>
        <!-- Page content goes here -->
        <header>
            <h1>Main Page Heading</h1>
        </header>
        <main>
            <p>This is a paragraph of text.</p>
        </main>
        <footer>
            <p>&copy; 2023 My Website</p>
        </footer>
    </body>
    </html>
    ```

*   **Headings**:
    ```html
    <h1>Heading Level 1 (Most important)</h1>
    <h2>Heading Level 2</h2>
    <h3>Heading Level 3</h3>
    <h4>Heading Level 4</h4>
    <h5>Heading Level 5</h5>
    <h6>Heading Level 6 (Least important)</h6>
    ```

*   **Paragraphs and Text Formatting**:
    ```html
    <p>This is a paragraph. It can contain <strong>bold text (strong importance)</strong>,
       <b>bold text (stylistic)</b>, <em>emphasized text (italic)</em>,
       <i>italic text (stylistic)</i>, <mark>marked/highlighted text</mark>,
       <small>small text</small>, <del>deleted text</del>, <ins>inserted text</ins>,
       <sub>subscript</sub>, and <sup>superscript</sup>.
    </p>
    <br> <!-- Line break (use sparingly) -->
    <hr> <!-- Thematic break (horizontal rule) -->
    <blockquote>
        <p>This is a blockquote, often used for long quotations.</p>
        <footer>—Author Name, <cite>Source Title</cite></footer>
    </blockquote>
    <pre>
    This is preformatted text.
    It preserves    white space
    and line breaks.
    <code>
    // Often used for code blocks
    function greet() {
      console.log("Hello");
    }
    </code>
    </pre>
    <p>Use <code>&lt;code&gt;</code> for inline code snippets.</p>
    ```

*   **Links (Anchors)**:
    ```html
    <a href="https://www.example.com">Visit Example.com (External Link)</a>
    <a href="/about.html">About Us (Internal Link)</a>
    <a href="#section1">Jump to Section 1 (Page Anchor)</a>
    <a href="mailto:info@example.com">Email Us</a>
    <a href="tel:+1234567890">Call Us</a>
    <a href="document.pdf" download>Download Document</a>
    <a href="https://www.example.com" target="_blank" rel="noopener noreferrer">Open in New Tab</a>
    ```

*   **Images**:
    ```html
    <img src="image.jpg" alt="Descriptive text for the image (important for accessibility)" width="300" height="200">
    <figure>
        <img src="complex-image.png" alt="Complex diagram description">
        <figcaption>Figure 1: A complex diagram explained.</figcaption>
    </figure>
    ```

*   **Lists**:
    *   Unordered List:
        ```html
        <ul>
            <li>First item</li>
            <li>Second item
                <ul>
                    <li>Nested item A</li>
                    <li>Nested item B</li>
                </ul>
            </li>
            <li>Third item</li>
        </ul>
        ```
    *   Ordered List:
        ```html
        <ol type="1" start="3"> <!-- type: 1, A, a, I, i -->
            <li>Item three</li>
            <li>Item four</li>
        </ol>
        ```
    *   Description List:
        ```html
        <dl>
            <dt>HTML</dt>
            <dd>HyperText Markup Language</dd>
            <dt>CSS</dt>
            <dd>Cascading Style Sheets</dd>
        </dl>
        ```

*   **Tables**:
    ```html
    <table>
        <caption>Monthly Sales</caption>
        <thead>
            <tr>
                <th scope="col">Month</th>
                <th scope="col">Product A Sales</th>
                <th scope="col">Product B Sales</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th scope="row">January</th>
                <td>150</td>
                <td>200</td>
            </tr>
            <tr>
                <th scope="row">February</th>
                <td>180</td>
                <td>220</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <th scope="row">Total</th>
                <td>330</td>
                <td>420</td>
            </tr>
        </tfoot>
    </table>
    ```

*   **Forms**:
    ```html
    <form action="/submit-form" method="post">
        <div>
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required minlength="4" placeholder="Enter your username">
        </div>
        <div>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
        </div>
        <div>
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" placeholder="you@example.com">
        </div>
        <div>
            <label for="age">Age:</label>
            <input type="number" id="age" name="age" min="18" max="99">
        </div>
        <div>
            <label for="bio">Bio:</label>
            <textarea id="bio" name="bio" rows="4" cols="50"></textarea>
        </div>
        <div>
            <label for="country">Country:</label>
            <select id="country" name="country">
                <option value="">--Please choose an option--</option>
                <option value="us">United States</option>
                <option value="ca">Canada</option>
            </select>
        </div>
        <fieldset>
            <legend>Choose your interests:</legend>
            <div>
                <input type="checkbox" id="coding" name="interests" value="coding">
                <label for="coding">Coding</label>
            </div>
            <div>
                <input type="checkbox" id="music" name="interests" value="music">
                <label for="music">Music</label>
            </div>
        </fieldset>
        <fieldset>
            <legend>Preferred contact method:</legend>
            <div>
                <input type="radio" id="contact_email" name="contact_method" value="email" checked>
                <label for="contact_email">Email</label>
            </div>
            <div>
                <input type="radio" id="contact_phone" name="contact_method" value="phone">
                <label for="contact_phone">Phone</label>
            </div>
        </fieldset>
        <div>
            <label for="profile_pic">Profile Picture:</label>
            <input type="file" id="profile_pic" name="profile_pic" accept="image/png, image/jpeg">
        </div>
        <input type="hidden" name="csrf_token" value="some_secret_token">
        <button type="submit">Submit</button>
        <button type="reset">Reset Form</button>
    </form>
    ```
    *   Common `input` types: `text`, `password`, `email`, `number`, `date`, `checkbox`, `radio`, `file`, `submit`, `reset`, `button`, `hidden`, `url`, `tel`, `search`, `color`, `range`.

*   **Semantic HTML5 Elements**: Provide meaning to the structure.
    *   `<header>`: Introductory content for a page or section.
    *   `<nav>`: Navigation links.
    *   `<main>`: The main content of the document. Only one per page.
    *   `<article>`: Self-contained content (e.g., blog post, news story).
    *   `<section>`: Thematic grouping of content.
    *   `<aside>`: Content tangentially related to the content around it (e.g., sidebar).
    *   `<footer>`: Footer content for a page or section.
    *   `<figure>` and `<figcaption>`: For images, diagrams, code, etc., with a caption.
    *   `<time>`: Represents a specific period in time.
        ```html
        <time datetime="2023-10-26T14:30:00">October 26, 2023, 2:30 PM</time>
        ```
    *   `<address>`: Contact information.
    *   `<details>` and `<summary>`: For creating interactive disclosure widgets.
        ```html
        <details>
            <summary>Click to see more details</summary>
            <p>Here are the hidden details.</p>
        </details>
        ```

## CSS (Cascading Style Sheets) - Styling & Layout

CSS is used to style HTML elements.

*   **Ways to Apply CSS**:
    1.  **External Stylesheet** (recommended): Linked via `<link>` tag in `<head>`.
        ```html
        <!-- In HTML <head> -->
        <link rel="stylesheet" href="styles.css">
        ```
        ```css
        /* In styles.css */
        body { font-family: Arial, sans-serif; }
        p { color: blue; }
        ```
    2.  **Internal Stylesheet**: Using `<style>` tag in `<head>`.
        ```html
        <head>
            <style>
                h1 { color: green; }
            </style>
        </head>
        ```
    3.  **Inline Styles**: Using the `style` attribute on an HTML element (use sparingly, low maintainability).
        ```html
        <p style="color: red; font-size: 12px;">This paragraph has inline styles.</p>
        ```

*   **CSS Selectors**: Target HTML elements to style.
    *   **Universal Selector**: `*` (selects all elements - use with caution for performance)
    *   **Type Selector (Element Selector)**: `p`, `h1`, `div`
    *   **Class Selector**: `.classname` (e.g., `<p class="highlight">...</p>` -> `.highlight { ... }`)
    *   **ID Selector**: `#idname` (e.g., `<div id="main-nav">...</div>` -> `#main-nav { ... }`) - IDs must be unique per page.
    *   **Attribute Selectors**:
        *   `[attribute]` (e.g., `a[target]`)
        *   `[attribute=value]` (e.g., `input[type="text"]`)
        *   `[attribute~=value]` (contains word)
        *   `[attribute|=value]` (starts with value- or value)
        *   `[attribute^=value]` (starts with value)
        *   `[attribute$=value]` (ends with value)
        *   `[attribute*=value]` (contains value)
    *   **Pseudo-classes**: Define a special state of an element.
        *   `:link`, `:visited` (for links)
        *   `:hover`, `:active`, `:focus` (user interaction)
        *   `:first-child`, `:last-child`, `:nth-child(n)`, `:nth-of-type(n)`
        *   `:not(selector)`
        ```css
        a:hover { text-decoration: underline; }
        input:focus { border-color: blue; }
        li:nth-child(odd) { background-color: #f0f0f0; }
        ```
    *   **Pseudo-elements**: Style a specific part of an element.
        *   `::before`, `::after` (insert content before/after an element's content)
        *   `::first-letter`, `::first-line`
        *   `::selection` (style user-selected text)
        ```css
        p::first-letter { font-size: 2em; font-weight: bold; }
        .important::before { content: "⚠️ "; color: red; }
        ```
    *   **Combinators**:
        *   Descendant selector (space): `article p` (selects all `p` elements inside `article`)
        *   Child selector (`>`): `ul > li` (selects `li` elements that are direct children of `ul`)
        *   Adjacent sibling selector (`+`): `h2 + p` (selects the first `p` element immediately following an `h2`)
        *   General sibling selector (`~`): `h2 ~ p` (selects all `p` elements that are siblings of and come after an `h2`)
    *   **Grouping Selectors**: `,` (e.g., `h1, h2, .title { color: navy; }`)

*   **The Box Model**: Every HTML element is a rectangular box.
    *   `content`: The actual content (text, image).
    *   `padding`: Space between content and border.
    *   `border`: Line around the padding.
    *   `margin`: Space outside the border, separating it from other elements.
    ```css
    .box {
        width: 200px;
        height: 100px;
        padding: 20px; /* 20px on all sides */
        /* padding: 10px 20px; /* 10px top/bottom, 20px left/right */
        /* padding: 5px 10px 15px 20px; /* top right bottom left */
        border: 1px solid black;
        margin: 15px;
        box-sizing: border-box; /* width & height include padding and border, not just content */
    }
    ```

*   **Common CSS Properties**:
    *   **Colors**:
        *   `color`: Text color.
        *   `background-color`: Background color.
        *   Values: named colors (`red`, `blue`), hex (`#FF0000`), RGB (`rgb(255, 0, 0)`), RGBA (`rgba(255, 0, 0, 0.5)`), HSL, HSLA.
    *   **Typography**:
        *   `font-family`: Specify font(s) (e.g., `"Arial", sans-serif`).
        *   `font-size`: (e.g., `16px`, `1.2em`, `1rem`, `10vw`).
        *   `font-weight`: `normal`, `bold`, `100`-`900`.
        *   `font-style`: `normal`, `italic`, `oblique`.
        *   `text-align`: `left`, `right`, `center`, `justify`.
        *   `line-height`: Space between lines of text.
        *   `text-decoration`: `none`, `underline`, `overline`, `line-through`.
        *   `text-transform`: `none`, `capitalize`, `uppercase`, `lowercase`.
    *   **Sizing and Spacing**:
        *   `width`, `height`.
        *   `min-width`, `max-width`, `min-height`, `max-height`.
        *   `margin`, `padding` (see Box Model).
    *   **Borders**:
        *   `border-width`, `border-style` (`solid`, `dotted`, `dashed`), `border-color`.
        *   Shorthand: `border: 1px solid #ccc;`
        *   `border-radius`: For rounded corners.
    *   **Display Property**: Controls how an element is rendered.
        *   `block`: Takes up full width available, starts on a new line (e.g., `div`, `p`, `h1`).
        *   `inline`: Takes up only as much width as necessary, does not start on a new line (e.g., `span`, `a`, `img`). Width/height, top/bottom margins/paddings often don't apply as expected.
        *   `inline-block`: Like inline, but respects width/height, margins/paddings.
        *   `none`: Element is not displayed and takes up no space.
        *   `flex`: Enables Flexbox layout for direct children.
        *   `grid`: Enables CSS Grid layout for direct children.
    *   **Positioning Property**:
        *   `static`: Default value. Follows normal document flow.
        *   `relative`: Positioned relative to its normal position. `top`, `right`, `bottom`, `left` properties work.
        *   `absolute`: Positioned relative to its nearest positioned ancestor (or to the initial containing block). Taken out of normal flow.
        *   `fixed`: Positioned relative to the viewport. Stays in the same place even when scrolling. Taken out of normal flow.
        *   `sticky`: Hybrid of `relative` and `fixed`. Behaves like `relative` until it hits a specified offset, then "sticks".
        *   With `relative`, `absolute`, `fixed`, `sticky`, use `top`, `right`, `bottom`, `left`, and `z-index` (stacking order).
    *   **Overflow**: How to handle content that overflows its container.
        *   `visible` (default), `hidden`, `scroll`, `auto`.
    *   **Visibility**: `visible`, `hidden` (element is hidden but still takes up space).
    *   **Opacity**: `opacity: 0.5;` (value from 0.0 to 1.0).
    *   **Box Shadow**: `box-shadow: 10px 5px 5px red;` (h-offset v-offset blur spread color inset)
    *   **Text Shadow**: `text-shadow: 2px 2px 5px grey;`

*   **Units**:
    *   Absolute: `px` (pixels), `cm`, `mm`, `in`, `pt`, `pc`.
    *   Relative:
        *   `%`: Relative to parent element's property.
        *   `em`: Relative to the font-size of the element itself (or parent for font-size).
        *   `rem`: Relative to the font-size of the root (`html`) element.
        *   `vw`: 1% of viewport width.
        *   `vh`: 1% of viewport height.
        *   `vmin`, `vmax`: 1% of viewport's smaller/larger dimension.

*   **Specificity**: Rules for which CSS declaration is applied if multiple rules target the same element.
    *   Order: Inline styles > ID selectors > Class/Attribute/Pseudo-class selectors > Type selectors > Universal selector.
    *   `!important` overrides all other declarations (use sparingly).
    *   Later rules in the stylesheet override earlier ones if specificity is equal.

*   **Flexbox (Flexible Box Layout)**: One-dimensional layout model for arranging items in rows or columns.
    *   **Container Properties (applied to the parent/flex container)**:
        *   `display: flex;` or `display: inline-flex;`
        *   `flex-direction`: `row` (default), `row-reverse`, `column`, `column-reverse`.
        *   `flex-wrap`: `nowrap` (default), `wrap`, `wrap-reverse`.
        *   `flex-flow`: Shorthand for `flex-direction` and `flex-wrap`.
        *   `justify-content`: Alignment along the main axis (`flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`).
        *   `align-items`: Alignment along the cross axis (`stretch` (default), `flex-start`, `flex-end`, `center`, `baseline`).
        *   `align-content`: Alignment of lines when there's extra space in the cross axis (for multi-line flex containers with `flex-wrap: wrap`) (`flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `stretch`).
    ```css
    .flex-container {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
        height: 300px;
        background-color: lightblue;
    }
    .flex-item {
        background-color: dodgerblue;
        color: white;
        padding: 20px;
        margin: 10px;
    }
    ```
    *   **Item Properties (applied to the children/flex items)**:
        *   `order`: `<integer>` (default 0).
        *   `flex-grow`: `<number>` (default 0) - how much item can grow.
        *   `flex-shrink`: `<number>` (default 1) - how much item can shrink.
        *   `flex-basis`: `<length> | auto` (default `auto`) - initial main size.
        *   `flex`: Shorthand for `flex-grow`, `flex-shrink`, `flex-basis`. (e.g., `flex: 1;` -> `flex-grow:1; flex-shrink:1; flex-basis:0%`)
        *   `align-self`: Overrides container's `align-items` for a single item (`auto`, `flex-start`, `flex-end`, `center`, `baseline`, `stretch`).

*   **CSS Grid Layout**: Two-dimensional layout system for rows and columns.
    *   **Container Properties (applied to the parent/grid container)**:
        *   `display: grid;` or `display: inline-grid;`
        *   `grid-template-columns`: Defines columns (e.g., `100px 1fr 2fr;`, `repeat(3, 1fr);`). `fr` unit represents a fraction of available space.
        *   `grid-template-rows`: Defines rows (e.g., `auto 100px minmax(50px, 200px);`).
        *   `grid-template-areas`: Defines named grid areas.
        *   `gap` (or `grid-gap`): Space between grid cells (e.g., `gap: 10px;` or `row-gap: 5px; column-gap: 15px;`).
        *   `justify-items`: Aligns items along the row (inline) axis (`start`, `end`, `center`, `stretch`).
        *   `align-items`: Aligns items along the column (block) axis (`start`, `end`, `center`, `stretch`).
        *   `place-items`: Shorthand for `align-items` and `justify-items`.
        *   `justify-content`: Aligns the grid itself within the container along the row axis (if grid is smaller than container).
        *   `align-content`: Aligns the grid itself within the container along the column axis.
        *   `place-content`: Shorthand for `align-content` and `justify-content`.
    ```css
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); /* Responsive columns */
        /* grid-template-columns: 1fr 2fr 1fr; */
        /* grid-template-rows: auto 200px; */
        gap: 15px;
        background-color: lightcoral;
        padding: 10px;
    }
    .grid-item {
        background-color: lightgoldenrodyellow;
        padding: 20px;
        text-align: center;
    }
    ```
    *   **Item Properties (applied to the children/grid items)**:
        *   `grid-column-start`, `grid-column-end`, `grid-row-start`, `grid-row-end`: Define item's position and span.
        *   `grid-column`: Shorthand for `grid-column-start / grid-column-end` (e.g., `grid-column: 1 / 3;` or `grid-column: span 2;`).
        *   `grid-row`: Shorthand for `grid-row-start / grid-row-end`.
        *   `grid-area`: Assigns item to a named grid area or is a shorthand for row/column start/end.
        *   `justify-self`: Overrides container's `justify-items` for a single item.
        *   `align-self`: Overrides container's `align-items` for a single item.
        *   `place-self`: Shorthand for `align-self` and `justify-self`.
    ```css
    .grid-item-1 {
        grid-column: 1 / span 2; /* Span 2 columns starting from line 1 */
        grid-row: 1;
    }
    .grid-item-header {
        grid-area: header; /* If using grid-template-areas */
    }
    ```

*   **Responsive Design (Media Queries)**: Apply different styles based on device characteristics (e.g., viewport width).
    ```css
    /* Default styles (mobile-first approach) */
    .container { width: 100%; }

    /* Tablet styles */
    @media (min-width: 768px) {
        .container { width: 80%; margin: 0 auto; }
        body { font-size: 18px; }
    }

    /* Desktop styles */
    @media (min-width: 1024px) {
        .container { width: 70%; max-width: 1200px; }
        .sidebar { display: block; } /* Show sidebar on larger screens */
    }

    @media print { /* Styles for printing */
        body { color: black; background: white; }
        nav, footer { display: none; }
    }
    ```

This provides a solid foundation for the HTML & CSS cheatsheet. I'll proceed with `tailwind_css.md`.The `html_css.md` cheatsheet has been successfully updated with detailed examples of HTML tags, CSS selectors, properties, and layout techniques like Flexbox and Grid, formatted as requested.

Next, I will enhance `tailwind_css.md`. This will involve providing more specific examples of utility classes for styling, layout, responsiveness, and states, demonstrating how they are used directly in HTML.
