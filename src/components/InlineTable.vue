<template>
  <v-card class="mx-auto mt-10" max-width="600" outlined>
    <v-card-title>Vuetify Inline Editor Table </v-card-title>
    <v-data-table
      :headers="headers"
      :items="desserts"
      :search="search"
      class="elevation-1"
      fixed-header
      height="350px"
    >
      <v-divider inset></v-divider>
      <template v-slot:top>
        <v-toolbar flat color="white">
          <div class="d-flex w-100">
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              dense
              outlined
              single-line
              hide-details
            ></v-text-field>
            <v-btn color="primary" class="ml-2 white--text" @click="addNew">
              <v-icon dark>mdi-plus</v-icon>Add
            </v-btn>
          </div>
        </v-toolbar>
      </template>
      <template #[`item.name`]="{ item }">
        <v-text-field
          v-model="editedItem.name"
          :hide-details="true"
          dense
          single-line
          :autofocus="true"
          v-if="item.id === editedItem.id"
        ></v-text-field>
        <span v-else>{{ item.name }}</span>
      </template>
      <template #[`item.calories`]="{ item }">
        <v-text-field
          v-model="editedItem.calories"
          :hide-details="true"
          dense
          single-line
          v-if="item.id === editedItem.id"
        ></v-text-field>
        <span v-else>{{ item.calories }}</span>
      </template>
      <template #[`item.actions`]="{ item }">
        <div v-if="item.id === editedItem.id">
          <v-icon color="red" class="mr-3" @click="close">
            mdi-window-close
          </v-icon>
          <v-icon color="green" @click="save"> mdi-content-save </v-icon>
        </div>
        <div v-else>
          <v-icon color="green" class="mr-3" @click="editItem(item)">
            mdi-pencil
          </v-icon>
          <v-icon color="red" @click="deleteItem(item)"> mdi-delete </v-icon>
        </div>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  name: "InlineTable",
  data: () => ({
    search: "",
    headers: [
      { text: "Dessert", value: "name", sortable: false },
      { text: "Calories", value: "calories", sortable: false },
      { text: "Actions", value: "actions", sortable: false, width: "100px" },
    ],
    desserts: [],
    editIndex: -1,
    editedItem: {
      id: 0,
      name: "",
      calories: 0,
    },
    defaultItem: {
      id: 0,
      name: "New Item",
      calories: 0,
    },
  }),
  created() {
    this.initialize();
  },
  methods: {
    initialize() {
      this.desserts = [
        { id: 1, name: "Frozen", calories: 120 },
        { id: 2, name: "Ice Cream", calories: 200 },
        { id: 3, name: "Eclair", calories: 128 },
        { id: 4, name: "Cupcake", calories: 140 },
        { id: 5, name: "Gingerbread", calories: 159 },
        { id: 6, name: "Jellybean", calories: 110 },
        { id: 7, name: "Lollipop", calories: 132 },
        { id: 8, name: "Honeycomb", calories: 45 },
      ];
    },
    editItem(item) {
      this.editIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
    },
    deleteItem(item) {
      const index = this.desserts.indexOf(item);
      confirm("Are you sure you want to delete this item?") &&
        this.desserts.splice(index, 1);
    },
    close() {
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editIndex = -1;
      }, 300);
    },
    addNew() {
      const addObj = Object.assign({}, this.defaultItem);
      addObj.id = this.desserts.length + 1;
      this.desserts.unshift(addObj);
      this.editedItem(addObj);
    },
    save() {
      if (this.editIndex > -1) {
        Object.assign(this.desserts[this.editIndex], this.editItem);
      }
      this.close();
    },
  },
};
</script>

<style>
</style>