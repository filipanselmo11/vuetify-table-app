<template>
  <div>
    <v-select label="Food Type" :items="items" v-model="foodType"></v-select>
    <v-data-table :headers="headers" :items="filteredItems">
        <template v-slot:scope="{ item }">
            <td>{{ item.name }}</td>
            <td>{{ item.type }}</td>
            <td>{{ item.calories }}</td>
        </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  name: "TableComponent",
  data: () => ({
    food: [
      { name: "Backchoi", type: "vegetable", calories: 100 },
      { name: "Pork", type: "meat", calories: 200 },
      { name: "Chicken Thigh", type: "meat", calories: 300 },
      { name: "Wartemelon", type: "fruit", calories: 10 },
    ],
    items: ["vegetable", "meat", "fruit"],
    headers: [
      { text: "Name", align: "left", value: "name" },
      { text: "Food Type", align: "left", value: "type" },
      { text: "Calories", align: "left", value: "caloires" },
    ],
    foodType: null,
  }),
  computed: {
    filteredItems() {
      return this.food.filter((i) => {
        return !this.foodType || i.type === this.foodType;
      });
    },
  },
};
</script>

<style>
</style>