# Vue.js Cheatsheet

Vue.js is a progressive JavaScript framework for building user interfaces. This cheatsheet covers core Vue concepts, template syntax, directives, reactivity, computed properties, watchers, components, props, events, slots, lifecycle hooks, and an introduction to the Composition API.

## Setup

*   **Via CDN (for quick testing)**:
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <title>My Vue App</title>
      <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script> <!-- Vue 3 -->
      <!-- For Vue 2: <script src="https://cdn.jsdelivr.net/npm/vue@2"></script> -->
    </head>
    <body>
      <div id="app">
        {{ message }}
        <button @click="changeMessage">Change Message</button>
      </div>

      <script>
        const { createApp } = Vue; // Vue 3
        // For Vue 2: new Vue({ el: '#app', data: { message: 'Hello Vue!' }});

        createApp({
          data() {
            return {
              message: 'Hello Vue!'
            }
          },
          methods: {
            changeMessage() {
              this.message = 'Message Changed!';
            }
          }
        }).mount('#app');
      </script>
    </body>
    </html>
    ```
*   **Using Vite (Recommended for new projects - Vue 3)**:
    ```bash
    npm create vite@latest my-vue-app -- --template vue
    # or
    # yarn create vite my-vue-app --template vue
    cd my-vue-app
    npm install
    npm run dev
    ```
*   **Using Vue CLI (for Vue 2 or Vue 3 projects with more complex setups)**:
    ```bash
    npm install -g @vue/cli
    # or
    # yarn global add @vue/cli
    vue create my-vue-project
    # Follow prompts to choose Vue version (2 or 3) and features.
    cd my-vue-project
    npm run serve # or yarn serve
    ```

## Vue Instance / Application (Vue 3 Options API)

```javascript
// main.js (or within a <script> tag)
const app = Vue.createApp({
  // Options:
  data() { // Reactive data
    return {
      message: "Hello from Vue!",
      count: 0,
      seen: true
    };
  },
  methods: { // Methods that can be called from the template or other methods
    increment() {
      this.count++;
    },
    greet(name) {
      return `Hello, ${name}!`;
    }
  },
  computed: { // Derived properties based on reactive data, cached
    reversedMessage() {
      return this.message.split('').reverse().join('');
    }
  },
  watch: { // Observe and react to data changes
    count(newValue, oldValue) {
      console.log(`Count changed from ${oldValue} to ${newValue}`);
    }
  },
  // Lifecycle Hooks (see below)
  created() {
    console.log('Vue instance created. Message is: ' + this.message);
  },
  mounted() {
    console.log('Vue instance mounted to the DOM.');
  }
});

app.mount('#app'); // Mounts the app to an HTML element with id="app"
```

## Template Syntax

*   **Text Interpolation (Mustache syntax)**:
    ```html
    <p>{{ rawHtml }}</p> <!-- Outputs rawHtml as plain text -->
    <p>Message: {{ message }}</p>
    <p>Using a method: {{ greet('Alice') }}</p>
    ```
*   **Raw HTML (`v-html`)**: Output actual HTML. **Use with caution (XSS risk if content is user-generated).**
    ```html
    <p v-html="rawHtml"></p> <!-- Data: rawHtml: '<span style="color:red;">Red Text</span>' -->
    ```
*   **Attribute Bindings (`v-bind` or shorthand `:`)**:
    ```html
    <img v-bind:src="imageSrc" :alt="imageAlt">
    <button :disabled="isButtonDisabled">Click Me</button>
    <div :class="{ active: isActive, 'text-danger': hasError }">Dynamic Classes</div>
    <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">Dynamic Styles</div>
    ```
*   **JavaScript Expressions**: Vue supports full JavaScript expressions inside data bindings.
    ```html
    <p>{{ count + 1 }}</p>
    <p>{{ message.split('').reverse().join('') }}</p>
    <div :id="'list-' + id"></div>
    ```

## Directives

Directives are special attributes with the `v-` prefix.
*   **`v-text`**: Updates the element's `textContent`. Similar to `{{ }}`.
    ```html
    <span v-text="message"></span>
    ```
*   **`v-once`**: Render the element and component once. Subsequent re-renders will treat them as static content.
    ```html
    <p v-once>This will never change: {{ message }}</p>
    ```
*   **Conditional Rendering**:
    *   `v-if`, `v-else-if`, `v-else`:
        ```html
        <p v-if="type === 'A'">Type A</p>
        <p v-else-if="type === 'B'">Type B</p>
        <p v-else>Not A or B</p>
        <!-- v-if is "real" conditional rendering; element is added/removed from DOM -->
        ```
    *   `v-show`: Toggles the element's `display` CSS property. Element is always rendered and remains in the DOM.
        ```html
        <p v-show="isVisible">Now you see me</p>
        ```
*   **List Rendering (`v-for`)**:
    ```html
    <ul> <!-- Array of strings -->
      <li v-for="(item, index) in items" :key="index">
        {{ index }} - {{ item }}
      </li>
    </ul>

    <ul> <!-- Array of objects -->
      <li v-for="user in users" :key="user.id">
        {{ user.name }} ({{ user.email }})
      </li>
    </ul>

    <div> <!-- Object iteration -->
      <span v-for="(value, key, index) in myObject" :key="key">
        {{ index }}. {{ key }}: {{ value }} <br>
      </span>
    </div>

    <div v-for="n in 5" :key="n">Number: {{ n }}</div> <!-- Range -->
    ```
    *   **`:key` is crucial** for Vue to track each node's identity for efficient updates.
*   **Event Handling (`v-on` or shorthand `@`)**:
    ```html
    <button v-on:click="counter += 1">Add 1</button>
    <button @click="greetUser('Alice')">Greet Alice</button>
    <form @submit.prevent="onSubmitForm"> <!-- .prevent is an event modifier -->
      <input @keyup.enter="submitOnEnter" v-model="textInput">
      <button type="submit">Submit</button>
    </form>
    ```
    *   **Event Modifiers**:
        *   `.stop`: Stop event propagation.
        *   `.prevent`: Prevent default behavior.
        *   `.capture`: Add event listener in capture mode.
        *   `.self`: Only trigger if event.target is the element itself.
        *   `.once`: Trigger handler at most once.
        *   `.passive`: Improves scroll performance on mobile.
    *   **Key Modifiers**: `.enter`, `.tab`, `.delete` (captures both "Delete" and "Backspace"), `.esc`, `.space`, `.up`, `.down`, `.left`, `.right`.
*   **Form Input Bindings (`v-model`)**: Creates two-way data binding on form inputs, textareas, and select elements.
    ```html
    <!-- Text input -->
    <input type="text" v-model="message">
    <p>Message is: {{ message }}</p>

    <!-- Multiline text -->
    <textarea v-model="multilineText"></textarea>

    <!-- Checkbox (single) -->
    <input type="checkbox" id="checkbox" v-model="isChecked">
    <label for="checkbox">{{ isChecked }}</label>

    <!-- Checkboxes (multiple, bound to array) -->
    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
    <label for="jack">Jack</label>
    <input type="checkbox" id="john" value="John" v-model="checkedNames">
    <label for="john">John</label>
    <p>Checked: {{ checkedNames }}</p> <!-- Data: checkedNames: [] -->

    <!-- Radio buttons -->
    <input type="radio" id="one" value="One" v-model="picked">
    <label for="one">One</label>
    <input type="radio" id="two" value="Two" v-model="picked">
    <label for="two">Two</label>
    <p>Picked: {{ picked }}</p>

    <!-- Select (single) -->
    <select v-model="selectedOption">
      <option disabled value="">Please select one</option>
      <option>A</option>
      <option value="B_val">B</option>
    </select>
    <p>Selected: {{ selectedOption }}</p>

    <!-- Select (multiple, bound to array) -->
    <select v-model="selectedMultiple" multiple>
      <option>Apple</option> <option>Banana</option> <option>Cherry</option>
    </select>
    <p>Selected: {{ selectedMultiple }}</p>
    ```
    *   **`v-model` Modifiers**:
        *   `.lazy`: Sync after `change` events instead of `input`.
        *   `.number`: Typecasts input string to a number.
        *   `.trim`: Trims whitespace from input.
*   **`v-bind` (recap, powerful for dynamic attributes)**:
    ```html
    <a :href="url">Link</a>
    <div :class="[isActive ? 'activeClass' : '', errorClass]">Array Syntax for Class</div>
    <div :style="[baseStyles, overridingStyles]">Array Syntax for Style</div>
    ```
*   **`v-slot` (for named slots and scoped slots in components)**: See Components section.
*   **`v-pre`**: Skip compilation for this element and all its children.
*   **`v-cloak`**: Remains on the element until the associated Vue instance finishes compilation. Useful with CSS rules like `[v-cloak] { display: none }` to hide uncompiled templates.

## Reactivity

Vue uses a reactivity system. When you modify reactive data (properties in `data()`), Vue automatically updates the DOM.

## Computed Properties

Derived values based on reactive data. They are cached and only re-evaluate when their reactive dependencies change.
```javascript
// In Vue instance options:
// data() { return { firstName: 'John', lastName: 'Doe' }; },
// computed: {
//   fullName() {
//     // 'this' points to the Vue instance
//     return `${this.firstName} ${this.lastName}`;
//   },
//   // Computeds can also have a setter (less common)
//   // fullNameWithSetter: {
//   //   get() { return `${this.firstName} ${this.lastName}`; },
//   //   set(newValue) {
//   //     const names = newValue.split(' ');
//   //     this.firstName = names[0];
//   //     this.lastName = names[names.length - 1];
//   //   }
//   // }
// }
```
```html
<p>Full Name: {{ fullName }}</p>
```

## Watchers

Perform actions in response to data changes. Useful for asynchronous operations or more complex logic than computed properties.
```javascript
// In Vue instance options:
// data() { return { question: '', answer: 'Questions usually contain a question mark. ;-)' }; },
// watch: {
//   // whenever question changes, this function will run
//   question(newQuestion, oldQuestion) {
//     if (newQuestion.includes('?')) {
//       this.getAnswer();
//     }
//   }
// },
// methods: {
//   async getAnswer() {
//     this.answer = 'Thinking...';
//     try {
//       const res = await fetch('https://yesno.wtf/api'); // Example API
//       this.answer = (await res.json()).answer;
//     } catch (error) {
//       this.answer = 'Error! Could not reach the API. ' + error;
//     }
//   }
// }
```
```html
<!-- <input v-model="question" /> <p>{{ answer }}</p> -->
```

## Class and Style Bindings

*   **Binding HTML Classes**:
    *   Object Syntax:
        ```html
        <div :class="{ active: isActive, 'text-danger': hasError }"></div>
        ```
    *   Array Syntax:
        ```html
        <div :class="[isActive ? activeClass : '', errorClass]"></div>
        <div :class="[{ active: isActive }, errorClass]"></div>
        ```
*   **Binding Inline Styles**:
    *   Object Syntax:
        ```html
        <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
        <!-- CSS property names can be camelCase or kebab-case (in quotes) -->
        <div :style="{ 'font-weight': 'bold', 'background-color': bgColor }"></div>
        ```
    *   Array Syntax (multiple style objects):
        ```html
        <div :style="[baseStyles, overridingStyles]"></div>
        ```

## Components

Reusable Vue instances with a name.
*   **Defining a Global Component (less common for larger apps)**:
    ```javascript
    // const app = Vue.createApp({});
    // app.component('my-component-name', {
    //   props: ['message'],
    //   template: `<h4>{{ message }}</h4>`
    // });
    // app.mount('#app');
    ```
    ```html
    <!-- <my-component-name message="Hello from component!"></my-component-name> -->
    ```
*   **Single File Components (`.vue` files - Recommended)**:
    Requires a build setup (Vite or Vue CLI).
    ```vue
    <!-- MyButton.vue -->
    <template>
      <button @click="handleClick" :style="{ backgroundColor: color }">
        <slot></slot> <!-- Default slot -->
        {{ buttonText }}
      </button>
    </template>

    <script>
    export default {
      name: 'MyButton',
      props: {
        buttonText: {
          type: String,
          default: 'Click Me'
        },
        color: String
      },
      emits: ['button-click'], // Declare emitted events (Vue 3)
      methods: {
        handleClick() {
          this.$emit('button-click', 'Button was clicked!'); // Emit custom event
        }
      }
    }
    </script>

    <style scoped> /* 'scoped' limits CSS to this component only */
    button {
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    </style>
    ```
    ```javascript
    // ParentComponent.vue (script part)
    // import MyButton from './MyButton.vue';
    // export default {
    //   components: { MyButton },
    //   methods: {
    //     onMyButtonClicked(payload) {
    //       alert(payload);
    //     }
    //   }
    // }
    ```
    ```html
    <!-- ParentComponent.vue (template part) -->
    <!-- <MyButton button-text="Submit Form" color="green" @button-click="onMyButtonClicked">
           <span>Icon</span> Send
         </MyButton> -->
    ```
*   **Props**: Pass data from parent to child.
    *   Prop names: kebab-case in template (`my-prop`), camelCase in script (`myProp`).
    *   Prop validation: `type`, `required`, `default`, `validator`.
*   **Emitting Events (`$emit`)**: Child components communicate with parents by emitting events.
*   **Slots**: For content distribution. Allows parent to pass template fragments into child component.
    *   Default Slot: `<slot></slot>`
    *   Named Slots:
        ```html
        <!-- ChildComponent.vue -->
        <!-- <div> <header><slot name="header"></slot></header> <main><slot></slot></main> <footer><slot name="footer"></slot></footer> </div> -->
        <!-- Parent -->
        <!-- <ChildComponent>
               <template v-slot:header> <h1>Page Title</h1> </template>
               <p>Main content.</p>
               <template #footer> <p>Copyright info</p> </template>  Shorthand #footer
             </ChildComponent> -->
        ```
    *   Scoped Slots: Slot content can access data from the child component.
        ```html
        <!-- ChildWithScopedSlot.vue -->
        <!-- <ul> <li v-for="item in items" :key="item.id"> <slot name="item" :item-data="item" :index="idx"></slot> </li> </ul> -->
        <!-- Parent -->
        <!-- <ChildWithScopedSlot :items="myList">
               <template v-slot:item="slotProps">
                 <span>{{ slotProps.index }}: {{ slotProps.itemData.name }}</span>
               </template>
             </ChildWithScopedSlot> -->
        ```

## Lifecycle Hooks (Options API)

Functions that execute at specific stages of a component's life.
Common hooks:
*   `beforeCreate()`
*   `created()`: Instance created, data observed, events set up. `this` is available.
*   `beforeMount()`
*   `mounted()`: Instance mounted to DOM. Element is available. Good for DOM manipulations or data fetching that needs DOM.
*   `beforeUpdate()`
*   `updated()`: Data changed, DOM re-rendered.
*   `beforeUnmount()` (Vue 3) / `beforeDestroy()` (Vue 2)
*   `unmounted()` (Vue 3) / `destroyed()` (Vue 2): Instance destroyed. Clean up timers, event listeners.

## Composition API (Vue 3)

Alternative to Options API for organizing component logic, especially in larger components.
*   **`setup()` function**: Entry point for Composition API. Executes before component instance is created. Receives `props` and `context` (includes `attrs`, `slots`, `emit`).
*   **Reactivity Functions**:
    *   `ref()`: Creates a reactive reference for a primitive value or an object. Access value with `.value`.
    *   `reactive()`: Creates a reactive proxy for an object.
    *   `computed()`: Create computed properties.
    *   `watch()` / `watchEffect()`: Create watchers.
*   **Lifecycle Hooks (Composition API)**: Imported from `vue`. e.g., `onMounted`, `onUpdated`, `onUnmounted`.
    ```vue
    <!-- MyComponentComposition.vue -->
    <template>
      <div>
        <p>Count: {{ count }}</p>
        <p>Double Count: {{ doubleCount }}</p>
        <button @click="increment">Increment</button>
      </div>
    </template>

    <script>
    import { ref, computed, onMounted, watch } from 'vue';

    export default {
      name: 'MyComponentComposition',
      props: {
        initialCount: {
          type: Number,
          default: 0
        }
      },
      setup(props, { emit }) {
        // Reactive state
        const count = ref(props.initialCount);

        // Computed property
        const doubleCount = computed(() => count.value * 2);

        // Method
        function increment() {
          count.value++;
          emit('count-changed', count.value);
        }

        // Watcher
        watch(count, (newVal, oldVal) => {
          console.log(`Count changed from ${oldVal} to ${newVal}`);
        });

        // Lifecycle hook
        onMounted(() => {
          console.log('Component is mounted (Composition API)');
        });

        // Expose to template
        return {
          count,
          doubleCount,
          increment
        };
      }
    }
    </script>
    ```

## Routing (Vue Router - Official Library)

Install: `npm install vue-router@4` (for Vue 3)
```javascript
// router/index.js
// import { createRouter, createWebHistory } from 'vue-router';
// import HomeView from '../views/HomeView.vue';
// const routes = [
//   { path: '/', name: 'Home', component: HomeView },
//   { path: '/about', name: 'About', component: () => import('../views/AboutView.vue') /* Lazy load */ }
// ];
// const router = createRouter({ history: createWebHistory(process.env.BASE_URL), routes });
// export default router;

// main.js
// import { createApp } from 'vue';
// import App from './App.vue';
// import router from './router';
// createApp(App).use(router).mount('#app');
```
```html
<!-- App.vue or any component -->
<!-- <nav>
       <router-link to="/">Home</router-link> |
       <router-link :to="{ name: 'About' }">About</router-link>
     </nav>
     <router-view/> Router outlet where matched component renders -->
```

## State Management (Pinia - Official Library for Vue 3)

Install: `npm install pinia`
```javascript
// stores/counter.js
// import { defineStore } from 'pinia';
// export const useCounterStore = defineStore('counter', {
//   state: () => ({
//     count: 0,
//     name: 'My Counter'
//   }),
//   getters: {
//     doubleCount: (state) => state.count * 2,
//   },
//   actions: {
//     increment() {
//       this.count++;
//     },
//     reset() {
//       this.count = 0;
//     }
//   },
// });

// main.js
// import { createApp } from 'vue';
// import { createPinia } from 'pinia';
// import App from './App.vue';
// const app = createApp(App);
// app.use(createPinia());
// app.mount('#app');

// MyComponent.vue (script setup syntax for Composition API)
// <script setup>
// import { useCounterStore } from '@/stores/counter';
// const counterStore = useCounterStore();
// // Access state: counterStore.count
// // Access getters: counterStore.doubleCount
// // Call actions: counterStore.increment()
// </script>
// <template>
//   <p>Count: {{ counterStore.count }}</p>
//   <p>Double: {{ counterStore.doubleCount }}</p>
//   <button @click="counterStore.increment()">Increment</button>
// </template>
```
Vuex is the official state management library for Vue 2, and can also be used with Vue 3.

This provides a solid Vue.js cheatsheet. I'll proceed with `regex.md`.The `vuejs.md` cheatsheet has been successfully updated with detailed code snippets and explanations for core Vue concepts, template syntax, directives, reactivity, computed properties, watchers, components (Options API and an introduction to Composition API with `setup`), props, events, slots, lifecycle hooks, and basic examples for Vue Router and Pinia.

Next, I will enhance `regex.md`, focusing on providing clear examples for each metacharacter, quantifier, group, assertion, and common patterns.
