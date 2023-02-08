<template>
  <v-card>
    <v-card-title>
      <span class="text-h5">Cliente</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="Nome*"
              v-model="nome"
              required
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="CPF*"
              v-model="cpf"
              required
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="Data de nascimento*"
              v-model="dataNasc"
              required
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
          >
            <v-text-field
              label="Endereço*"
              v-model="endereco"
              required
            ></v-text-field>
          </v-col>
        </v-row>
      </v-container>
      <small>*Campos obrigatórios</small>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        color="blue-darken-1"
        variant="text"
        @click="close"
      >
        Fechar
      </v-btn>
      <v-btn
        color="blue-darken-1"
        variant="text"
        @click="save"
      >
        Salvar
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: "ClienteForm",
  emits: ["save", "close"],

  data() {
    return {
      id: null,
      nome: '',
      cpf: '',
      dataNasc: '',
      endereco: ''
    };
  },
  methods: {
    save() {
      const dataCliente = {
        id: this.id,
        nome: this.nome,
        cpf: this.cpf,
        data_nasc: new Date(this.dataNasc),
        endereco: this.endereco,
      };
      this.$emit('save', dataCliente);
    },
    edit(cliente) {
      this.id = cliente.id;
      this.nome = cliente.nome;
      this.cpf = cliente.cpf;
      this.dataNasc = cliente.data_nasc;
      this.endereco = cliente.endereco;
    },
    close() {
      this.nome = '';
      this.cpf = '';
      this.dataNasc = '';
      this.endereco = '';
      this.$emit('close');
    },
  },
};
</script>
