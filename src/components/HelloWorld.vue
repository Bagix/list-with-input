<template>
  <div class="container">
    <my-input @sendItem="addNewItem" class="wrapper"></my-input>
    <ul class="menu">
      <li v-for="(item, index) in items" 
      :key="index" 
      v-on:click="getText(item.name, index)"
      v-bind:class="{highlight: index === activeItem}">
        {{ item.name }}
        </li>
    </ul>
    <h1 class="message">Wybrałeś zakładkę: <span class="text-highlight">{{ text }}</span></h1>
  </div>
</template>

<script>
import MyInput from '@/components/Input.vue'

export default {
  name: 'NavigationMenu',
  components: {
    'my-input': MyInput
  },
  data() {
    return {
      text: '',
      activeItem: '',
      items: [
        {name: 'Postacie'},
        {name: 'Zwierzęta'},
        {name: 'Miasta'},
        {name: 'Przedmioty'},
        {name: 'Rośliny'},
      ]
    }
  },
  methods: {
    getText: function(text, index) {
      this.text = text
      this.activeItem = index;
    },
    addNewItem: function(newItem) {
      this.items.push({'name': newItem})
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  :root {
    --highlight: rgb(240, 93, 178);
    --highlight-dark: rgb(230, 83, 168);
    --normal: rgb(69, 183, 228);
    --normal-dark: rgb(59, 173, 218);
  }
  .container {
    width: 100%;
    max-width: 1200px;
    margin: auto;
    padding-top: 3rem;
  }

  .wrapper {
    margin: 1rem 0;
  }
  
  .menu {
    display: flex;
    border-radius: 3px;
    list-style: none;
    width: 100%;
    max-width: 700px;
    margin: 0 auto;
    padding: 0;
    flex-direction: column;
    background-color: var(--normal);
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .menu > li {
    padding: 1rem 2rem;
    color: #fff;
    font-weight: bold;
    cursor: pointer;
    transition: all .2s linear;
  }

  .menu > li:hover {
    color: var(--highlight);
  }

  .message {
    margin-top: 3rem;
  }

  .text-highlight {
    color: var(--highlight);
  }

  .highlight {
    background-color: var(--highlight);
    color: #fff;
  }

  .menu > li.highlight:hover {
    color: #fff;
  }

  @media (min-width: 768px) {
    .menu {
      flex-direction: row;
    }
  }
</style>
