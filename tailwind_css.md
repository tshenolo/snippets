# Tailwind CSS Cheatsheet

Tailwind CSS is a utility-first CSS framework for rapidly building custom user interfaces. Instead of predefined components, Tailwind provides low-level utility classes that you compose directly in your HTML.

## Core Concepts

*   **Utility-First**: Style elements by applying pre-existing classes directly in your HTML.
*   **Responsive Design**: Use screen prefix variants (e.g., `md:`, `lg:`) to apply utilities at specific breakpoints.
*   **States**: Use state variants (e.g., `hover:`, `focus:`, `active:`) to style elements in different states.
*   **Dark Mode**: Use the `dark:` variant for dark mode styles.
*   **Customization**: Highly customizable via the `tailwind.config.js` file.
*   **Just-In-Time (JIT) Compiler**: Generates styles on-demand as you write your classes, leading to smaller CSS bundles in development and production. (Default in Tailwind CSS v3.0+)

## Setup

*   **Via CDN (for quick testing, not recommended for production)**:
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <script src="https://cdn.tailwindcss.com"></script>
      <script>
        // Optional: Customize Tailwind via CDN (limited)
        tailwind.config = {
          theme: {
            extend: {
              colors: {
                clifford: '#da373d',
              }
            }
          }
        }
      </script>
    </head>
    <body>
      <h1 class="text-3xl font-bold text-clifford underline">Hello world!</h1>
    </body>
    </html>
    ```
*   **As a PostCSS Plugin (Recommended for Projects)**:
    1.  Install Tailwind CSS and its peer dependencies:
        ```bash
        npm install -D tailwindcss postcss autoprefixer
        # or
        # yarn add -D tailwindcss postcss autoprefixer
        ```
    2.  Initialize Tailwind (creates `tailwind.config.js` and `postcss.config.js`):
        ```bash
        npx tailwindcss init -p
        ```
    3.  Configure `tailwind.config.js` to include paths to all your template files:
        ```javascript
        // tailwind.config.js
        module.exports = {
          content: [
            "./src/**/*.{html,js,jsx,ts,tsx,vue}", // Adjust paths based on your project structure
            "./public/index.html",
          ],
          theme: {
            extend: {},
          },
          plugins: [],
        }
        ```
    4.  Include Tailwind directives in your main CSS file (e.g., `src/input.css`):
        ```css
        @tailwind base;
        @tailwind components;
        @tailwind utilities;
        ```
    5.  Compile your CSS:
        ```bash
        npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch
        # (Add this to your package.json scripts)
        ```
    6.  Link the compiled CSS in your HTML:
        ```html
        <link href="/dist/output.css" rel="stylesheet">
        ```

## Layout Utilities

*   **Container**: Centers content with responsive max-widths.
    ```html
    <div class="container mx-auto px-4"> <!-- mx-auto for horizontal centering, px-4 for padding -->
      <!-- Content -->
    </div>
    ```
*   **Display**: `block`, `inline-block`, `inline`, `flex`, `inline-flex`, `grid`, `inline-grid`, `hidden`, `table`, etc.
    ```html
    <div class="block ...">Block Element</div>
    <span class="inline ...">Inline Element</span>
    <div class="flex ...">Flex Container</div>
    <div class="hidden ...">This is hidden</div>
    ```
*   **Positioning**: `static`, `relative`, `absolute`, `fixed`, `sticky`.
    *   With positioning, use inset utilities: `top-0`, `left-4`, `bottom-auto`, `right-1/2`, etc.
    ```html
    <div class="relative">
      <div class="absolute top-0 right-0 p-2 bg-red-500 text-white">Absolute</div>
    </div>
    <div class="fixed bottom-0 left-0 w-full bg-gray-800 text-white p-4">Fixed Footer</div>
    ```
*   **Visibility**: `visible`, `invisible` (hides but still takes up space).
*   **Z-Index**: `z-0`, `z-10`, `z-20`, `z-auto`, etc.
*   **Overflow**: `overflow-auto`, `overflow-hidden`, `overflow-visible`, `overflow-scroll`, `overflow-x-scroll`, `overflow-y-auto`.

## Flexbox

Apply to a flex container (`display: flex` or `display: inline-flex`).
*   **Flex Direction**: `flex-row`, `flex-row-reverse`, `flex-col`, `flex-col-reverse`.
*   **Flex Wrap**: `flex-nowrap`, `flex-wrap`, `flex-wrap-reverse`.
*   **Justify Content** (main axis alignment): `justify-start`, `justify-end`, `justify-center`, `justify-between`, `justify-around`, `justify-evenly`.
*   **Align Items** (cross axis alignment): `items-stretch`, `items-start`, `items-end`, `items-center`, `items-baseline`.
*   **Align Self** (for individual flex items): `self-auto`, `self-start`, `self-end`, `self-center`, `self-stretch`, `self-baseline`.
*   **Flex Grow/Shrink/Basis**: `flex-grow`, `flex-grow-0`, `flex-shrink`, `flex-shrink-0`, `flex-basis-auto`, `flex-basis-0`, `flex-basis-1/2`, etc.
*   **Flex Shorthand**: `flex-1` (flex: 1 1 0%), `flex-auto` (flex: 1 1 auto), `flex-initial` (flex: 0 1 auto), `flex-none` (flex: none).
*   **Gap**: `gap-4`, `gap-x-2`, `gap-y-8` (space between flex/grid items).
    ```html
    <div class="flex flex-row justify-center items-center gap-4 p-4 bg-slate-200">
      <div class="flex-1 p-4 bg-blue-500 text-white">Item 1 (Grows)</div>
      <div class="p-4 bg-green-500 text-white">Item 2</div>
      <div class="flex-none p-4 bg-yellow-500 text-black">Item 3 (No Grow/Shrink)</div>
    </div>
    ```

## Grid

Apply to a grid container (`display: grid` or `display: inline-grid`).
*   **Grid Template Columns**: `grid-cols-1`, `grid-cols-3`, `grid-cols-none`, `grid-cols-[200px_1fr_minmax(0,1fr)]` (arbitrary values).
*   **Grid Template Rows**: `grid-rows-2`, `grid-rows-layout` (if defined in config), `grid-rows-[auto_1fr_auto]`.
*   **Grid Column Start/End**: `col-auto`, `col-span-1`, `col-span-2`, `col-span-full`, `col-start-2`, `col-end-5`.
*   **Grid Row Start/End**: `row-auto`, `row-span-1`, `row-span-3`, `row-start-1`, `row-end-4`.
*   **Gap**: `gap-4`, `gap-x-2`, `gap-y-8`.
    ```html
    <div class="grid grid-cols-3 gap-4 p-4 bg-rose-200">
      <div class="col-span-2 p-4 bg-purple-500 text-white">Item A (spans 2 cols)</div>
      <div class="p-4 bg-purple-500 text-white">Item B</div>
      <div class="p-4 bg-purple-500 text-white">Item C</div>
      <div class="col-start-1 col-end-4 p-4 bg-purple-700 text-white">Item D (spans full width)</div>
    </div>
    ```

## Sizing

*   **Width**: `w-0`, `w-px`, `w-1` (0.25rem), `w-1/2` (50%), `w-full` (100%), `w-screen` (100vw), `w-auto`, `w-min` (min-content), `w-max` (max-content), `w-fit` (fit-content).
*   **Height**: `h-0`, `h-px`, `h-1`, `h-1/2`, `h-full` (100%), `h-screen` (100vh), `h-auto`.
*   **Min/Max Width/Height**: `min-w-0`, `max-w-xs`, `min-h-screen`, `max-h-full`.

## Spacing

*   **Padding**: `p-0`, `p-1` (0.25rem), `px-2` (horizontal), `py-3` (vertical), `pt-4` (top), `pr-5` (right), `pb-6` (bottom), `pl-7` (left).
*   **Margin**: `m-0`, `m-1`, `mx-auto` (horizontal auto), `my-3`, `mt-4`, `mr-5`, `mb-6`, `ml-7`.
    *   Negative margins: `-m-1`, `-mt-2`.
*   **Space Between** (for direct children, useful for flex/grid items if gap is not used or for other elements): `space-x-4`, `space-y-2`, `space-x-reverse`.
    ```html
    <div class="flex space-x-4">
      <div>Item 1</div>
      <div>Item 2</div>
      <div>Item 3</div>
    </div>
    ```

## Typography

*   **Font Family**: `font-sans`, `font-serif`, `font-mono`. (Configurable in `tailwind.config.js`).
*   **Font Size**: `text-xs`, `text-sm`, `text-base` (default), `text-lg`, `text-xl`, `text-2xl` ... `text-9xl`.
*   **Font Weight**: `font-thin`, `font-extralight`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `font-extrabold`, `font-black`.
*   **Text Color**: `text-black`, `text-white`, `text-red-500`, `text-blue-700`, `text-transparent`. (Extensive color palette).
*   **Text Align**: `text-left`, `text-center`, `text-right`, `text-justify`.
*   **Line Height**: `leading-none`, `leading-tight`, `leading-snug`, `leading-normal`, `leading-relaxed`, `leading-loose`.
*   **Letter Spacing**: `tracking-tighter`, `tracking-tight`, `tracking-normal`, `tracking-wide`, `tracking-wider`, `tracking-widest`.
*   **Text Decoration**: `underline`, `overline`, `line-through`, `no-underline`.
*   **Text Transform**: `uppercase`, `lowercase`, `capitalize`, `normal-case`.
*   **Text Overflow**: `truncate` (ellipsis for single line), `text-ellipsis`, `text-clip`.
*   **Whitespace**: `whitespace-normal`, `whitespace-nowrap`, `whitespace-pre`, `whitespace-pre-line`, `whitespace-pre-wrap`.

## Backgrounds

*   **Background Color**: `bg-transparent`, `bg-black`, `bg-white`, `bg-red-500`, `bg-gradient-to-r from-purple-500 to-pink-500`.
*   **Background Image**: `bg-none`, `bg-cover`, `bg-contain`, `bg-center`, `bg-repeat`, `bg-fixed`. (Often used with custom images defined in `tailwind.config.js`).
    ```html
    <div class="bg-cover bg-center h-64" style="background-image: url('/path/to/image.jpg')"></div>
    ```

## Borders

*   **Border Width**: `border`, `border-0`, `border-2`, `border-t-4` (top only), `border-x-2` (left and right).
*   **Border Color**: `border-transparent`, `border-black`, `border-red-500`.
*   **Border Style**: `border-solid`, `border-dashed`, `border-dotted`, `border-double`, `border-none`.
*   **Border Radius**: `rounded-none`, `rounded-sm`, `rounded`, `rounded-md`, `rounded-lg`, `rounded-full`, `rounded-t-xl` (top only).
*   **Divide Utilities** (for borders between elements): `divide-x`, `divide-y`, `divide-gray-300`.
    ```html
    <div class="flex divide-x divide-gray-400">
      <div class="p-4">Item 1</div>
      <div class="p-4">Item 2</div>
    </div>
    ```

## Effects & Filters

*   **Box Shadow**: `shadow-sm`, `shadow`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`, `shadow-inner`, `shadow-none`.
*   **Opacity**: `opacity-0`, `opacity-25`, `opacity-50`, `opacity-75`, `opacity-100`.
*   **Filters**:
    *   Blur: `blur-sm`, `blur-md`.
    *   Brightness: `brightness-50`, `brightness-100`.
    *   Contrast: `contrast-50`, `contrast-125`.
    *   Grayscale: `grayscale`.
    *   Hue Rotate: `hue-rotate-90`.
    *   Invert: `invert`.
    *   Saturate: `saturate-50`, `saturate-150`.
    *   Sepia: `sepia`.
*   **Backdrop Filters** (apply filters to the area behind an element): `backdrop-blur-sm`, `backdrop-brightness-50`.

## Transitions & Animations

*   **Transition Property**: `transition`, `transition-colors`, `transition-opacity`, `transition-shadow`, `transition-transform`, `transition-all`.
*   **Transition Duration**: `duration-75`, `duration-100`, `duration-1000`.
*   **Transition Timing Function**: `ease-linear`, `ease-in`, `ease-out`, `ease-in-out`.
*   **Transition Delay**: `delay-75`, `delay-1000`.
*   **Animation**: `animate-none`, `animate-spin`, `animate-ping`, `animate-pulse`, `animate-bounce`. (Define custom animations in `tailwind.config.js`).
    ```html
    <button class="transition-colors duration-300 ease-in-out bg-blue-500 hover:bg-blue-700 text-white p-2 rounded">
      Hover Me
    </button>
    <div class="animate-spin h-10 w-10 border-4 border-blue-500 border-t-transparent rounded-full"></div>
    ```

## Interactivity

*   **Cursor**: `cursor-auto`, `cursor-default`, `cursor-pointer`, `cursor-wait`, `cursor-not-allowed`.
*   **User Select**: `select-none`, `select-text`, `select-all`, `select-auto`.
*   **Appearance**: `appearance-none` (remove default browser styling for form elements).

## Responsive Design (Prefixes)

Apply utilities at specific breakpoints. Default breakpoints (customizable):
*   `sm`: 640px
*   `md`: 768px
*   `lg`: 1024px
*   `xl`: 1280px
*   `2xl`: 1536px

```html
<!-- Mobile first: text-center, then text-left on medium screens and up -->
<div class="text-center md:text-left">Content</div>

<!-- Hidden on mobile, block on large screens and up -->
<div class="hidden lg:block">Desktop Only Content</div>

<!-- Different padding values for different screen sizes -->
<div class="p-4 sm:p-6 md:p-8">Responsive Padding</div>

<!-- Flex column on mobile, row on medium screens -->
<div class="flex flex-col md:flex-row">
  <div>Item 1</div>
  <div>Item 2</div>
</div>
```

## State Variants (Prefixes)

Style elements based on their state.
*   **Hover**: `hover:bg-blue-700`, `hover:text-white`
*   **Focus**: `focus:ring-2`, `focus:outline-none`
*   **Active**: `active:bg-green-600`
*   **Visited** (for links): `visited:text-purple-600`
*   **Disabled** (for form elements): `disabled:opacity-50`, `disabled:cursor-not-allowed`
*   **Group Hover/Focus**: Style children when a parent with `group` class is hovered/focused.
    ```html
    <a href="#" class="group block max-w-xs mx-auto rounded-lg p-6 bg-white ring-1 ring-slate-900/5 shadow-lg space-y-3 hover:bg-sky-500 hover:ring-sky-500">
      <div class="flex items-center space-x-3">
        <h3 class="text-slate-900 group-hover:text-white text-sm font-semibold">New Project</h3>
      </div>
      <p class="text-slate-500 group-hover:text-white text-sm">Create a new project from a variety of starting templates.</p>
    </a>
    ```
*   **Peer States**: Style an element when a sibling element (marked with `peer`) has a certain state.
    ```html
    <input type="checkbox" class="peer sr-only" id="toggle">
    <label for="toggle" class="block w-10 h-6 bg-gray-300 rounded-full p-1 peer-checked:bg-blue-500 transition-colors">
      <span class="block w-4 h-4 bg-white rounded-full transform peer-checked:translate-x-4 transition-transform"></span>
    </label>
    ```
*   **Dark Mode (`dark:`)**:
    ```html
    <div class="bg-white dark:bg-slate-800 text-slate-700 dark:text-slate-300">
      This changes appearance in dark mode.
    </div>
    ```
    (Requires dark mode to be enabled in `tailwind.config.js`, e.g., `darkMode: 'class'` or `darkMode: 'media'`)

## Customization (`tailwind.config.js`)

```javascript
// tailwind.config.js
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    screens: { // Override default screens
      'sm': '576px',
      'md': '768px',
      'lg': '992px',
      'xl': '1200px',
    },
    colors: { // Extend or override colors
      transparent: 'transparent',
      current: 'currentColor',
      'white': '#ffffff',
      'purple': '#3f3cbb',
      'midnight': '#121063',
      'metal': '#565584',
      'tahiti': { // Nested colors
        100: '#cffafe',
        DEFAULT: '#06b6d4', // 'tahiti' class will use this
        900: '#083344',
      },
    },
    extend: { // Add new utilities or extend existing ones
      spacing: {
        '128': '32rem',
      },
      fontFamily: {
        'display': ['Oswald', 'sans-serif'],
        'body': ['"Open Sans"', 'sans-serif'],
      },
      animation: {
        'fade-in': 'fadeIn 1s ease-out forwards',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        }
      }
    },
  },
  plugins: [
    // require('@tailwindcss/forms'),
    // require('@tailwindcss/typography'),
  ],
}
```

## Directives

Used in your CSS file.
*   `@tailwind base;`: Injects Tailwind's base styles and any base styles registered by plugins.
*   `@tailwind components;`: Injects Tailwind's component classes and any component classes registered by plugins.
*   `@tailwind utilities;`: Injects Tailwind's utility classes and any utility classes registered by plugins.
*   `@layer base|components|utilities { ... }`: Tell Tailwind which "bucket" your custom styles belong to, controlling their order relative to Tailwind's own styles.
    ```css
    @layer base {
      h1 { @apply text-2xl; } /* Apply existing utilities */
      a { @apply text-blue-600 underline; }
    }
    @layer components {
      .btn-primary {
        @apply py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75;
      }
    }
    ```
*   `@apply`: Inline existing utility classes into your custom CSS. Use sparingly; prefer composing utilities in HTML.
*   `theme()`: Access values from your `tailwind.config.js` theme in your CSS.
    ```css
    .my-custom-component {
      background-color: theme('colors.purple');
      padding: theme('spacing.128');
    }
    ```

This provides a more comprehensive Tailwind CSS cheatsheet. I'll proceed with `react.md`.The `tailwind_css.md` cheatsheet has been successfully updated with detailed examples of utility classes for layout, spacing, typography, backgrounds, borders, effects, responsive design, and state variants, along with setup and customization notes.

Next, I will enhance `react.md`, focusing on providing actionable code snippets for components (functional and class-based, though emphasizing functional with hooks), JSX, props, state management (`useState`, `useEffect`), event handling, conditional rendering, lists, forms, and common hooks.
