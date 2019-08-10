<template>

  <v-flex id="fondo-motorista">
<v-layout align-center justify-center fill-height class="mx-5 my-5">

  
  <v-data-table :headers="headers" :items="motoristas" class="elevation-1" >
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-toolbar-title>MOTORISTAS</v-toolbar-title>

        <v-divider class="mx-4" inset vertical></v-divider>

        <v-spacer></v-spacer>

        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on }">
            <v-btn color="primary" dark class="mb-2" v-on="on">Novo Motorista</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container grid-list-md>
                <v-layout wrap>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.name" label="Nome"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.birth_date" label="Data de nascimento"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.state" label="Estado"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.city" label="Cidade"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.country" label="País"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.neighborhood" label="Bairro"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.city" label="Cidade"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.street_name" label="Nome da Rua"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.street_number" label="N*"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.postal_code" label="CEP"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.addresses.complement" label="Complemento"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.expires_at" label="Expiração"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.country" label="Pais"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.number" label="Numero"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.doc_type" label="Tipo de Documento"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.category" label="Categoria"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.nacionality" label="Nacionalidade"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.number2" label="Numero de Documento"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.documents.doc_type2" label="Tipo de Documento"></v-text-field>
                  </v-flex>
                  <v-flex sm2 xs9 class="mx-4">
                                        <v-switch color="primary" v-model="motoristas.active"
                                            :label="`Motorista: ${motoristas.active ? 'ativo' : 'inativo'}`">
                                        </v-switch>
                                    </v-flex>



                </v-layout>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="save">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>

     <template v-slot:item.ati="{ item }" >
      <td :v-text="`${motoristas.active ? 'ativo' : 'inativo'}`"/>
    </template>

    <template v-slot:item.action="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
      <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
    </template>

    <template>
      <v-btn color="primary" @click="initialize">Reset</v-btn>
    </template>
  </v-data-table>


</v-layout>
  <v-flex md12>
    <v-btn> Voltar </v-btn>
  </v-flex>
  <v-flex>
    <v-btn> Gostou ?</v-btn>
    </v-flex>
  </v-flex>

</template>
<script>
export default {
  data: () => ({
    
    dialog: false,
    sortable: false,
    headers: [
      {
        text: "Nome",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "Data de nascimento", 
        value: "birth_date",
        sortable: false },

      { text: "Cidade",
        value: "city",
        sortable: false },
        
      {
        text: "Tipo de Documento",
        value: "documents.doc_type",
        sortable: false
      },
      { text: "Categoria", value: "documents.category", sortable: false },
      { text: "Actions", value: "action", sortable: false },
      { text: "motorista", value: "ati", sortable: false }
   
   ],
    motoristas: [],
    editedIndex: -1,
    editedItem: {
      ati: 'ativo',
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
      ati: 'ativo',
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
      this.motoristas = [
        {ati: 'ativo',
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
      this.editedIndex = this.motoristas.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      const index = this.motoristas.indexOf(item);
      confirm("Tem certeza de apagar este motorista?") &&
        this.motoristas.splice(index, 1);
    },

    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.motoristas[this.editedIndex], this.editedItem);
      } else {
        this.motoristas.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>
<style scoped>
#fondo-motorista{
background-color: rgba(255, 255, 0, 0.267);

margin-left:  100px;
margin-right: 100px;
}
</style>
