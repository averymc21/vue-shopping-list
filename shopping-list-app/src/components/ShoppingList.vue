<template>
    <div class="shopping-list">
      <h1>Shopping List</h1>
      <form @submit.prevent="addItem">
        <input v-model="newItem" placeholder="Add an item" />
        <button type="submit">Add</button>
      </form>
      <ul>
        <li v-for="(item, index) in items" :key="index" :class="{ found: item.found }">
          <!-- Use a span to wrap the item name for better click targeting -->
          <span @click="toggleFound(index)">{{ item.name }}</span>
          <button @click.stop="removeItem(index)">Remove</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ShoppingList',
    data() {
      return {
        newItem: '', // Input for new item
        items: [], // List of items
      };
    },
    methods: {
      // Add new item to the list
      addItem() {
        if (this.newItem.trim() !== '') {
          this.items.push({ name: this.newItem.trim(), found: false }); // Add new item with `found` set to false
          this.newItem = ''; // Clear the input field
        }
      },
      // Remove item from the list
      removeItem(index) {
        this.items.splice(index, 1);
      },
      // Toggle the `found` status of an item
      toggleFound(index) {
        this.items[index].found = !this.items[index].found;
      },
    },
  };
  </script>
  
  <style scoped>
/* Colors from the Coolors palette */

.shopping-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #073B4C; /* Light blue background */
  color: #FFFFFF; /* Dark blue text color */
  border: 1px solid #118AB2; /* Dark blue border */
  border-radius: 5px;
}

/* Form styling */
form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

/* Input styling */
input {
  flex: 1;
  padding: 8px;
  border: 1px solid #118AB2; /* Dark blue border */
  border-radius: 3px;
  color: #073B4C; /* Dark blue text color */
}

/* Button styling */
button {
  padding: 8px 15px;
  background-color: #EF476F; /* Pink button background */
  color: #FFFFFF; /* White text color */
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

/* Button hover effect */
button:hover {
  background-color: #FFD166; /* Yellow button background on hover */
}

/* List styling */
ul {
  list-style-type: none;
  padding: 0;
}

/* List item styling */
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 5px;
  background-color: #FFFFFF; /* White background */
  border: 1px solid #118AB2; /* Dark blue border */
  border-radius: 3px;
  color: #073B4C; /* Dark blue text color */
}

/* Apply strike-through to item name */
li.found span {
  text-decoration: line-through;
  color: #06D6A0; /* Green slash color */
}

/* Remove button styling */
button.remove-button {
  padding: 5px 10px;
  background-color: #06D6A0; /* Green button background */
  color: #FFFFFF; /* White text color */
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

/* Remove button hover effect */
button.remove-button:hover {
  background-color: #FFD166; /* Yellow button background on hover */
}
</style>
