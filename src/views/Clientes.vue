<template>
  <v-dialog
    v-model="dialog"
  >
    <ClienteForm ref="clienteForm" @save="save" @close="dialog = false"></ClienteForm>
  </v-dialog>
  <v-table>
    <thead>
      <tr>
        <th>
          ID
        </th>
        <th>
          Nome
        </th>
        <th>
          CPF
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="cliente in clientes" :key=cliente.id>
        <td>
          {{ cliente.id }}
        </td>
        <td>
          {{ cliente.nome }}
        </td>
        <td>
          {{ cliente.cpf }}
        </td>
      </tr>
    </tbody>
  </v-table>
  <v-btn @click="dialog = true">Cadastrar cliente</v-btn>
</template>
<script>
import axios from 'axios';
import ClienteForm from '@/components/ClienteForm.vue'
export default {
  name: "Clientes",
  components: { ClienteForm },
  data() {
    return {
      clientes: [],
      dialog: false,
    };
  },
  methods: {
    async getClientes() {
      try {
        const res = await axios.get("/api/clientes/");
        this.clientes = res.data;
      } catch (error) {
        console.log("Erro ao buscar clientes: " + error)
      }
    },
    async save(cliente) {
      try {
        let id = cliente.id;
        delete cliente.id;

        if (id) {
          await axios.put("/api/clientes/" + id + "/",cliente);
        } else {
          await axios.post("/api/clientes/",cliente);
        }
        this.dialog = false;
      } catch (error) {
        console.log("Erro ao salvar cliente: " + error);
      }
    }
  },
  async mounted() {
    await this.getClientes();
  },
};
</script>
