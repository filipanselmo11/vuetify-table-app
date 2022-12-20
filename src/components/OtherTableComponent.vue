<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="items"
      class="elevation-1"
      show-select
    >
      <template v-slot[`item.name`]="{ item, index, header }">
        <v-text-field
          :value="item.index"
          outlined
          dense
          @input="
            (payload) =>
              setField({
                item: item,
                value: payload,
                index: index,
                prop: 'name',
              })
          "
        >
          <template v-slot:label>
            <field-label :label="header.text"></field-label>
          </template>
        </v-text-field>
      </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  name: "OtherTableComponent",
  data: () => ({
    headers: [
      {
        text: "Nome",
        value: "nome",
      },
      {
        text: "SMS",
        value: "sms",
      },
      {
        text: "WhatsApp",
        value: "whatsapp",
      },
      {
        text: "Grupo de WhatsApp",
        value: "grupo",
      },
    ],
    items: [
      {
        nome: "Naruto",
        sms: "71272181287-219129128",
        whatsapp: "12321321-123123",
        grupo: "123213-21312312",
      },
      {
        nome: "Goku",
        sms: "1232134132-12312313123",
        whatsapp: "12323uy81623712687-1231231223",
        grupo: "12312312312-213123123",
      },
      {
        nome: "Ichigo",
        sms: "12321213-123321",
        whatsapp: "213123434234-21323123",
        grupo: "654336545-3453534543",
      },
      {
        nome: "Sanji",
        sms: "123123123-12312312",
        whatsapp: "323212-1221123",
        grupo: "1231231201212312312-12312132",
      },
    ],
  }),
  methods: {
    // setField({ item = {}, value = null, prop = "", index = null }) {
    //   const indexEmpty = ["", null, undefined].indexOf(index) != -1;
    //   //  if (indexEmpty !item !prop) {
    //   //     return;
    //   //  }
    //   const hasProp = item.hasOwnProperty(prop);

    //   if (hasProp) {
    //     item[prop] = value;
    //     Vue.set(this.items, index, item);
    //   }
    // },
  },
};
</script>

<style>
</style>