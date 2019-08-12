<template>
  <v-flex id="fondo-motorista" class="mx-5 my-5">
    <v-layout align-center justify-center fill-height class="my-5">
      <v-data-table
        id="table-background"
        :headers="headers"
        :items="drivers"
        class="elevation-5 mt-5 mx-5"
      >
        <template v-slot:top>
          <v-toolbar class="elevation-5" flat color id="tabela">
            <v-toolbar-title id="titulo">MOTORISTAS</v-toolbar-title>

            <v-divider class="mx-4" inset vertical></v-divider>

            <v-spacer></v-spacer>

            <v-dialog v-model="dialog" max-width="500px">
              <template v-slot:activator="{ on }">
                <v-btn id="botoes" dark class="mb-2 elevation-5" v-on="on">Novo Motorista</v-btn>
              </template>

              <v-card id="tabela" dark>
                <v-card-title>
                  <span class="headline">{{ formTitle }}</span>

                  <v-spacer></v-spacer>

                  <v-icon class="mb-5" @click="close">mdi-close</v-icon>
                </v-card-title>

                <v-card-text>
                  <v-container grid-list-md>
                    <v-layout wrap>
                      <v-flex xs12>
                        <span style="color:white; font-size:18px">Dados Pessoais:</span>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.name"
                          label="Nome"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.birth_date"
                          label="Data de nascimento"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md5>
                        <v-text-field
                          v-model="editedItem.state"
                          label="Estado"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md7>
                        <v-text-field
                          v-model="editedItem.city"
                          label="Cidade"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12>
                        <span style="color:white; font-size:18px">Endereço:</span>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.addresses.neighborhood"
                          label="Bairro"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.addresses.city"
                          label="Cidade"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md5>
                        <v-text-field
                          v-model="editedItem.addresses.country"
                          label="País"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md7>
                        <v-text-field
                          v-model="editedItem.addresses.street_name"
                          label="Nome da Rua"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm3 md2>
                        <v-text-field
                          v-model="editedItem.addresses.street_number"
                          label="N*"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="editedItem.addresses.postal_code"
                          label="CEP"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field v-model="editedItem.addresses.complement" label="Complemento"></v-text-field>
                      </v-flex>

                      <v-flex xs12>
                        <span style="color:white; font-size:18px">Documentos:</span>
                      </v-flex>

                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="editedItem.documents.expires_at"
                          label="Expiração"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="editedItem.documents.country"
                          label="Pais"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="editedItem.documents.number"
                          label="Numero"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.documents.doc_type"
                          label="Tipo de Documento"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.documents.category"
                          label="Categoria"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12>
                        <span style="color:white; font-size:18px">Documentos do País:</span>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.documents.nacionality"
                          label="Nacionalidade"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.documents.number2"
                          label="Numero de Documento"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex xs12 sm6 md6>
                        <v-text-field
                          v-model="editedItem.documents.doc_type2"
                          label="Tipo de Documento"
                          :rules="[rules.required]"
                          name="input-10-2"
                          class="input-group--focused"
                        ></v-text-field>
                      </v-flex>

                      <v-flex sm2 xs9 class="mx-4">
                        <v-switch
                          color="primary"
                          v-model="editedItem.active"
                          :label="`Motorista: ${editedItem.active ? 'ativo' : 'inativo'}`"
                        ></v-switch>
                      </v-flex>
                    </v-layout>
                  </v-container>
                </v-card-text>

                <v-card-actions>
                  <v-spacer></v-spacer>

                  <v-btn text @click="close">Cancel</v-btn>
                  <v-btn text @click="save">Save</v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-toolbar>
        </template>

        <template v-slot:item.active="{ item }">
          <td v-text="`${item.active ? 'ativo' : 'inativo'}`" />
        </template>

        <template v-slot:item.action="{ item }" v-slot:activator="{ on }">
          <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
          <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
      </v-data-table>
    </v-layout>

    <v-layout align-center justify-center row fill-height>
      <v-btn id="botoes" dark class="mx-5 my-5 elevation-5" href="/">Voltar</v-btn>
      <a
        href="https://api.whatsapp.com/send?1=pt_BR&amp;phone=5567992615784"
        target="_blank"
        style="text-decoration:none"
      >
        <v-btn id="botoes" dark class="mx-5 my-5 elevation-5">
          Gostou ?
          <v-icon color="red">mdi-heart</v-icon>
        </v-btn>
      </a>
    </v-layout>
  </v-flex>
</template>
<script>
export default {
  data: () => ({
    dialog: false,
    rules: {
      required: value => !!value || "Obrigatorio."
    },
    headers: [
      {
        text: "Nome",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "Data de nascimento", value: "birth_date", sortable: false },

      { text: "Cidade", value: "city", sortable: false },

      {
        text: "Tipo de Documento",
        value: "documents.doc_type",
        sortable: false
      },
      { text: "Categoria", value: "documents.category", sortable: false },
      { text: "Actions", value: "action", sortable: false },
      { text: "motorista", value: "active", sortable: false }
    ],
    driver: {
      addresses: {},
      documents: {}
    },
    drivers: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      birth_date: "",
      state: "",
      city: "",
      addresses: {
        name: "",
        state: "",
        country: "",
        neighborhood: "",
        city: "",
        street_number: "",
        complement: "",
        postal_code: "",
        street_name: ""
      },
      documents: {
        expires_at: "",
        country: "",
        number: "",
        doc_type: "",
        category: "",

        nacionality: "",
        number: "",
        doc_type2: ""
      }
    },
    defaultItem: {
      name: "",
      birth_date: "",
      state: "",
      city: "",
      addresses: {
        name: "",
        state: "",
        country: "",
        neighborhood: "",
        city: "",
        street_number: "",
        complement: "",
        postal_code: "",
        street_name: ""
      },
      documents: {
        expires_at: "",
        country: "",
        number: "",
        doc_type: "",
        category: "",

        nacionality: "",
        number: "",
        doc_type2: ""
      }
    }
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Novo Motorista" : "Editar Motorista";
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    }
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.drivers = [
        {
          active: true,
          name: "Pouca Tripa",
          birth_date: "1976-09-22T00:00:00",
          state: "São Paulo",
          city: "São Paulo",
          addresses: {
            state: "São Paulo",
            country: "BR",
            neighborhood: "CENTRO",
            city: "São Paulo",
            street_number: 24,
            complement: "apartamento",
            postal_code: "01300-000",
            street_name: "Avenida Paulista"
          },

          documents: {
            expires_at: "2010-11-23T00:00:00+00:00",
            country: "BR",
            number: "700441702",
            doc_type: "CNH",
            category: "AB",

            nacionality: "BR",
            number2: "32132132188",
            doc_type2: "CPF"
          }
        },
        {
          active: false,
          name: "Quase nada",
          birth_date: "1986-09-22T00:00:00",
          state: "Rio de Janeiro",
          city: "Niterói",
          addresses: {
            state: "",
            country: "",
            neighborhood: "",
            city: "",
            street_number: "",
            complement: "",
            postal_code: "",
            street_name: ""
          },
          documents: {
            expires_at: "",
            country: "",
            number: "",
            doc_type: "",
            category: "",

            nacionality: "BR",
            number2: "12312312377",
            doc_type2: "CPF"
          }
        }
      ];
    },

    editItem(item) {
      this.editedIndex = this.drivers.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      const index = this.drivers.indexOf(item);
      confirm("Tem certeza de apagar este motorista?") &&
        this.drivers.splice(index, 1);
    },
    close() {
      this.dialog = false;
      setTimeout(() => {
        this.driver = {
          addresses: {},
          documents: {}
        };
        this.editedIndex = -1;
      }, 300);
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.drivers[this.editedIndex], this.editedItem);
      } else {
        this.drivers.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>
<style scoped>
#fondo-motorista {
  background-color: rgba(255, 255, 0, 0.267);
}

#tabela {
  border-radius: 15px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  border: solid 1px;
  background-color: rgb(56, 95, 115);
}

#table-background {
  border-radius: 20px;
  background-color: rgba(255, 255, 255, 0.664);
}

#botoes {
  border-radius: 20px;
}

#titulo {
  color: white;
  text-shadow: 1px 1px black;
}
</style>
