<template>
  <div>
    <h1>{{ titulo }}</h1>
    <button @click="buscar()" class="btn btn-lith" style="float:left">Filtro</button>
    <input type="search" style="float:left" v-model="textToSearch" @input="buscar()">
    <br><br> <br> 
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Correo electrónico</th>
          <th>Dirección</th>
          <th>Teléfono</th>
          <th>País</th>
          <th>Ciudad</th>
          <th></th>
        </tr>
        <tr>
          <th><button @click="agregarPersona()">Agregar</button></th>
          <th><input type="text" v-model="personaNuevaObj.name"></th>
          <th><input type="text" v-model="personaNuevaObj.email"></th>
          <th><input type="text" v-model="personaNuevaObj.address"></th>
          <th><input type="text" v-model="personaNuevaObj.phone"></th>
          <th><input type="text" v-model="personaNuevaObj.country"></th>
          <th><input type="text" v-model="personaNuevaObj.city"></th>
          <th></th>
        </tr>
        <tr v-if="indexParaEditar !== null">
          <th><button @click="guardarPersona()">Guardar</button></th>
          <th><input type="text" v-model="personaEditarObj.name"></th>
          <th><input type="text" v-model="personaEditarObj.email"></th>
          <th><input type="text" v-model="personaEditarObj.address"></th>
          <th><input type="text" v-model="personaEditarObj.phone"></th>
          <th><input type="text" v-model="personaEditarObj.country"></th>
          <th><input type="text" v-model="personaEditarObj.city"></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(persona, index) in personas" :key="persona.id">
          <td>{{ persona.id }}</td>
          <td>{{ persona.name }}</td>
          <td>{{ persona.email }}</td>
          <td>{{ persona.address }}</td>
          <td>{{ persona.phone }}</td>
          <td>{{ persona.country }}</td>
          <td>{{ persona.city }}</td>
          <td>
            <button @click="elimintarPersona(index)">Eliminar</button>
            <button @click="editarPersona(persona, index)">Editar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'MiComponente',
  data() {
    return {
      titulo: 'Registro de Personas',
      personaNuevaObj: {
        id: 6,
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: ""
      },
      personaEditarObj: {
        id: null,
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: ""
      },
      indexParaEditar: null,
      textToSearch: "",
      personas: [],
      personasOriginales: [] // Datos originales
    };
  },
  mounted() {
    // Inicializar con datos 
    this.personasOriginales = [
      {
        id: 1,
        name: "Alice Johnson",
        email: "alice.johnson@example.com",
        address: "123 Maple Street",
        phone: "123-456-7890",
        country: "USA",
        city: "New York"
      },
      {
        id: 2,
        name: "Bob Smith",
        email: "bob.smith@example.com",
        address: "456 Oak Avenue",
        phone: "987-654-3210",
        country: "Canada",
        city: "Toronto"
      },
      {
        id: 3,
        name: "Carol White",
        email: "carol.white@example.com",
        address: "789 Pine Road",
        phone: "555-123-4567",
        country: "UK",
        city: "London"
      },
      {
        id: 4,
        name: "David Brown",
        email: "david.brown@example.com",
        address: "321 Elm Street",
        phone: "444-555-6666",
        country: "Australia",
        city: "Sydney"
      },
      {
        id: 5,
        name: "Emily Davis",
        email: "emily.davis@example.com",
        address: "654 Spruce Lane",
        phone: "333-444-5555",
        country: "USA",
        city: "Los Angeles"
      }
    ];
    // Copia de datos originales a personas
    this.personas = [...this.personasOriginales];
  },
  methods: {
    agregarPersona() {
      this.personas.push(this.personaNuevaObj);
      this.personaNuevaObj = {
        id: this.personas.length + 1,
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: ""
      };
    },
    elimintarPersona(index) {
      this.personas.splice(index, 1);
    },
    editarPersona(persona, index) {
      this.indexParaEditar = index;
      this.personaEditarObj = Object.assign({}, persona);
    },
    guardarPersona() {
      this.personas[this.indexParaEditar] = Object.assign({}, this.personaEditarObj);
      this.indexParaEditar = null;
    },
    buscar() {
      const searchText = this.textToSearch.toLowerCase();
      if (searchText === "") {
        this.personas = [...this.personasOriginales];
      } else {
        this.personas = this.personasOriginales.filter(persona =>
          persona.name.toLowerCase().includes(searchText) || persona.email.toLowerCase().includes(searchText)
        );
      }
    }
  }
}
</script>

<style scoped>
h1 {
  color: #42b983;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
}
th {
  background-color: #f2f2f2;
  text-align: left;
}

/* Estilo del botón de filtro */
button.btn-lith {
  background-color: #44bd98; 
  color: white; 
  padding: 5px 15px; 
  border: none; 
  border-radius: 5px; 
  cursor: pointer;
  font-size: 1em; 
  font-weight: bold; 
  transition: background-color 0.3s ease, transform 0.3s ease; 
  margin-right: 10px; 
}

/* Estilo de los botones dentro de la tabla */
button {
  padding: 10px 15px; 
  border: none; 
  border-radius: 5px;
  cursor: pointer; 
  font-size: 0.9em; 
  font-weight: bold; 
  transition: background-color 0.3s ease, transform 0.3s ease; 
  margin: 0 5px; 
  background-color: #d5e6dc;
}


/* Estilo para la tabla */
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 10px;
}

th {
  background-color: #f2f2f2;
  text-align: left;
}

tbody tr:nth-child(even) {
  background-color: #f9f9f9; 
}

tbody tr:hover {
  background-color: #f1f1f1; 
}

</style>
