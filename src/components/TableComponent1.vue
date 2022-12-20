<template>
  <div>
    <button @click="addRow">Add Rows</button>
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Celular</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(usuario, index) in usuarios" :key="index">
          <td>
            <input v-model="usuario.nome" class="form-control" type="text" />
          </td>
          <td>
            <input v-model="usuario.celular" class="form-control" type="text" />
          </td>
          <td>
            <input v-model="usuario.email" class="form-control" type="text" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TableComponent1",
  data: () => ({
    usuarios: [
      {
        nome: "Fílip",
        celular: "12312312321",
        email: "filip@email.com",
      },
      {
        nome: "Fílip",
        celular: "12312312321",
        email: "filip@email.com",
      },
      {
        nome: "Fílip",
        celular: "12312312321",
        email: "filip@email.com",
      },
    ],
  }),
  methods: {
    addRow() {
      this.usuarios.push({ nome: "", celular: "", email: "" });
    },
  },
};
</script>

<style>
</style>