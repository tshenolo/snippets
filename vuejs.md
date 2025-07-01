# Vue.js Cheatsheet

*   **Core Concepts**: Progressive framework, components, template syntax, reactivity.
*   **Setup**: CDN, Vue CLI, Vite.
*   **Vue Instance / Application**: `createApp()`.
*   **Template Syntax**:
    *   Text Interpolation: `{{ message }}`.
    *   Raw HTML: `v-html`.
    *   Attribute Bindings: `v-bind:id` or `:id`.
    *   JavaScript Expressions: Inside `{{ }}` and `v-bind`.
*   **Directives**: `v-if`, `v-else`, `v-else-if`, `v-show`, `v-for`, `v-on:click` or `@click`, `v-model`, `v-bind`, `v-slot`.
*   **Reactivity**: Data properties in `data()` option.
*   **Computed Properties**: `computed` option, cached based on reactive dependencies.
*   **Watchers**: `watch` option, perform actions in response to data changes.
*   **Class and Style Bindings**: `:class`, `:style`.
*   **Event Handling**: `@click`, `@submit`, event modifiers (`.prevent`, `.stop`).
*   **Forms**: `v-model` for two-way data binding on form inputs.
*   **Components**:
    *   Definition: Single File Components (`.vue` files: `<template>`, `<script>`, `<style>`).
    *   Props: Declaring and passing data to child components.
    *   Emitting Events: `$emit` from child to parent.
    *   Slots: For content distribution.
*   **Lifecycle Hooks**: `created`, `mounted`, `updated`, `unmounted`, etc. (Options API vs Composition API).
*   **Composition API (Vue 3+)**: `setup()` function, `ref`, `reactive`, `computed`, `watch`, lifecycle hooks (e.g., `onMounted`).
*   **Routing (Vue Router)**: `createRouter`, `routes` configuration, `<router-link>`, `<router-view>`.
*   **State Management (Pinia / Vuex)**: For larger applications.
