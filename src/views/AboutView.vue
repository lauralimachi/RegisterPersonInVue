<template>
  <div>
    <h1>Rendering Lists with v-for</h1>
    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item }}</li>
    </ul>
    <button @click="addItem">Add Item</button>
  </div>
</template>

<script>
export default {
    data() {
        return {
            items: ['Item 1', 'Item 2', 'Item 3'],
        };
    },
    methods: {
        addItem() {
            this.items.push(`Item ${this.items.length + 1}`);
        },
    },
};
</script>

<style scoped>
h1 {
    color: #42b983;
}
button {
    margin-top: 10px;
}
</style>