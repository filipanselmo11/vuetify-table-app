<template>
  <div>
    <v-data-table :headers="headers" :items="items">
      <template #[`item.name`]="{ item }">
        <v-chip color="orange">
          {{ item.name }}
        </v-chip>
      </template>
      <template #[`item.status`]="{ item }">
        <v-switch v-model="item.status" @click.stop="showDialog = true">
          <template v-slot:label>
            <span v-if="item.status"> Ativo </span>
            <span v-else> Inativo </span>
          </template>
        </v-switch>
      </template>
    </v-data-table>
    <status-dialog
        :visible="showDialog"
        @close="showDialog=false"
    ></status-dialog>
  </div>
</template>

<script>
import StatusDialog from "./StatusDialog.vue";
export default {
  name: "FinalTableComponent",
  components: { StatusDialog },
  data: () => ({
    showDialog: false,
    headers: [
      { text: "Name", value: "name" },
      { text: "status", value: "status" },
    ],
    items: [
      { name: "Naruto", status: true },
      { name: "Itachi", status: false },
      { name: "Goku", status: true },
      { name: "Hinata", status: false },
      { name: "Robin", status: true },
      { name: "Miss Valentine", status: false },
    ],
  }),
  methods: {
    consoleStatus(status) {
      console.log(status);
    },
  },
};
</script>

<style scoped>
</style>