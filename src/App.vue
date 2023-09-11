<template>
  <div>
    <!-- 1. Template Syntax -->
    <!-- a. Text Interpolation -->
    <p>{{ message }}</p>
    <!-- b. Raw HTML [v-html] -->
    <div v-html="htmlContent"> </div>
    <!-- c. Attribute Bindings [v-bind:id] -->
    <button :id="btnId">Click me</button>
    <!-- d. JavaScript expressions inside syntax i.e.{{ }} -->
    <p>{{ 2 + 2 }}</p>
    

    <!-- 2. Methods -->
    <button @click="sayHello">Say Hello</button>
    

    <!-- 3. Reactivity Fundamentals -->
    <p>{{ count }}</p>
    

    <!-- 4. Computed Properties -->
    <p>Computed Property: {{ computedValue }}</p>
    
    <!-- 5. Class and Style Bindings -->
    <!-- a. Binding HTML class [v-bind:class] -->
    <div :class="{ active: isActive }"> Active Div </div>
    <!-- b. Binding Inline Styles [v-bind:style] -->
    <div :style="{ color: textColor }"> Styled Div </div>
    

    <!-- 6. List Rendering -->
    <!-- a. v-for with an Object -->
    <ul>
      <li v-for="(value, key) in items" :key="key">{{ key }}: {{ value }}</li>
    </ul> 
    <!-- b. v-for with a Range -->
    <ul>
      <li v-for="n in 5" :key="n">{{ n }}</li>
    </ul>
    <!-- c. v-for on <template> -->
      <div v-for="item in listItem" :key="item.id">
      <template>
        <p>{{ item.name }}</p>
        <span>Description: {{ item.description }}</span>
      </template>
    </div>
    <!-- d. v-for with v-if -->
    <ul>
      <li v-for="item in filteredItems" :key="item.id">{{ item.name }}</li>
    </ul>
    <!-- e. v-for with a Component -->
    <custom-component v-for="item in items" :key="item.id" :data="item"></custom-component>
    

    <!-- 7. Event Handling: Listening to Events [v-on:click] -->
    <!-- a. Inline Handlers -->
    <button @click="incrementCount">Increment Count</button>
    <!-- b. Method Handlers -->
    <button @click="handleClick">Handle Click</button>
    

    <!-- 8. Form Input Bindings -->
    <!-- a. v-model with various input types -->
    <input type="text" v-model="textValue" />
    <input type="checkbox" v-model="isChecked" />
    <input type="radio" value="option1" v-model="radioValue" />
    <select v-model="selectedOption">
      <option value="option1">Option 1</option>
      <option value="option2">Option 2</option>
    </select>
    <textarea v-model="textareaValue"></textarea>
    <!-- b. v-model modifiers -->
    <input type="text" v-model.trim="trimmedText" />
    
    
    <!-- 9. Watchers -->
    <!-- Watcher example in the script section -->
    
    <!-- 10. Components -->
    <!-- a. Props -->
    <child-component :propValue="parentValue"></child-component>
    
    <!-- b. Events [$emit] -->
    <child-component @child-event="handleChildEvent"></child-component>
    
    <!-- c. Slots -->
    <custom-layout>
      <p>This content goes into the slot</p>
    </custom-layout>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  data() {
    return {
      // 1. Template Syntax
      message: 'Hello, Vue!',
      htmlContent: '<p>Rendered as raw HTML</p>',
      btnId: 'myButtonId',
      
      items: [
        { id: 1, name: 'Item 1', description: 'Description for Item 1' },
        { id: 2, name: 'Item 2', description: 'Description for Item 2' },
        // Add more items as needed
      ],

      // 2. Methods
      sayHello() {
        alert('Hello!');
      },
      
      // 3. Reactivity Fundamentals
      count: ref(0),
      
      // 4. Computed Properties
      valueA: ref(5),
      valueB: ref(10),
      computedValue: computed(() => this.valueA + this.valueB),
      
      // 5. Class and Style Bindings
      isActive: ref(true),
      textColor: ref('red'),
      
      // 6. List Rendering
      listItem: {
        item1: 'Value 1',
        item2: 'Value 2',
      },
      filteredItems: [
        { id: 1, name: 'Item 1' },
        { id: 2, name: 'Item 2' },
        { id: 3, name: 'Item 3', show: true },
      ],
      
      // 8. Form Input Bindings
      textValue: ref(''),
      isChecked: ref(false),
      radioValue: ref(''),
      selectedOption: ref('option1'),
      textareaValue: ref(''),
      trimmedText: ref(''),
      
      // 10. Components
      parentValue: 'Data from parent',
    };
  },
  methods: {
    // 7. Event Handling: Listening to Events
    // b. Method Handlers
    handleClick() {
      alert('Button Clicked');
    },
    
    // 9. Watchers
    // Watcher example
    watchCount() {
      watch(() => this.count, (newVal, oldVal) => {
        console.log(`Count changed from ${oldVal} to ${newVal}`);
      });
    },
    
    // 10. Components
    // b. Events [$emit]
    handleChildEvent(data) {
      console.log('Received from child:', data);
    },
  },
};
</script>

<style>
/* 5. Class and Style Bindings */
.active {
  font-weight: bold;
}
</style>
