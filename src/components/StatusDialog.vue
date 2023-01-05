<template>
  <v-dialog v-model="show" max-width="500px">
    <v-card>
      <v-card-title>Título do Dialog</v-card-title>
      <v-card-text> Texto do Dialog..... </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" @click.stop="show = false"> Close </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "StatusDialog",
  props: ["visible"],
  computed: {
    show: {
      get() {
        return this.visible;
      },
      set(value) {
        if (!value) {
          this.$emit("close");
        }
      },
    },
  },
};
</script>

<style>
</style>