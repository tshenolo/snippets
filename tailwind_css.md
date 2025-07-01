# Tailwind CSS Cheatsheet

*   **Core Concept**: Utility-first CSS framework.
*   **Setup**: Installation (CDN, npm/yarn), configuration file (`tailwind.config.js`).
*   **Applying Classes**: Directly in HTML elements.
*   **Layout**:
    *   Containers: `container`.
    *   Display: `block`, `inline-block`, `inline`, `flex`, `grid`, `hidden`.
    *   Positioning: `static`, `fixed`, `absolute`, `relative`, `sticky`.
    *   Flexbox: `flex`, `flex-row`, `flex-col`, `items-center`, `justify-between`, `flex-grow`, `flex-shrink`.
    *   Grid: `grid`, `grid-cols-*`, `grid-rows-*`, `gap-*`, `col-span-*`.
*   **Styling**:
    *   Sizing: `w-*` (width), `h-*` (height), `p-*` (padding), `m-*` (margin).
    *   Typography: `font-*`, `text-*` (size, color, alignment).
    *   Backgrounds: `bg-*` (color, image).
    *   Borders: `border`, `border-*` (color, width, style), `rounded-*`.
    *   Shadows: `shadow-*`.
*   **Responsiveness**: Prefixes for breakpoints (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`). Example: `md:text-lg`.
*   **States**: Prefixes for hover, focus, active, etc. (`hover:bg-blue-700`, `focus:ring`).
*   **Customization**: Modifying `tailwind.config.js` (theme, variants, plugins).
*   **Directives**: `@tailwind`, `@apply`, `@layer`.
