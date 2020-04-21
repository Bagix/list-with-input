<template>
  <div class="tutja">
    <input type="text" name="new_item" v-model="new_item"/>
    <button type="button" v-on:click="addNewItem" class="btn">Dodaj</button>
    <p class="error" v-if="hasError">At least 3 signs!</p>
  </div>
</template>

<script>
export default {
  name: 'MyInput',
  data() {
    return {
      new_item: '',
      hasError: false,
    }
  },
  methods: {
    addNewItem: function() {
      if(this.new_item !== '' || this.new_item.length >= 3) {
        let new_item = this.new_item.charAt(0).toUpperCase() + this.new_item.slice(1)
        this.$emit('sendItem', new_item)
        this.hasError = false; // In case if previously there was an error.
        this.new_item = ''
      } else {
        this.hasError = true;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  input[type=text] {
    padding: .33rem;
    border: 1px solid #cdcdcd;
    border-radius: 3px;
  }

  .btn {
    background-color:rgb(69, 183, 228);
    cursor: pointer;
    color: #fff;
    padding: .5rem 1rem;
    font-weight: bold;
    margin: .5rem;
    border-radius: 3px;
    border: none;
    box-shadow: 0 0 1px 0 var(--normal-dark);
    transition: all .2s linear;
  }

  .btn:hover {
    background-color: var(--highlight-dark);
    box-shadow: 0 0 1px 0 var(--highlight-dark);
  }

  .error {
    color: crimson;
    font-weight: bold;
    text-decoration: underline;
  }

</style>
