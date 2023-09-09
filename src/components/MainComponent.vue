<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
  <div>
    <ul class="list-group container">
      <li v-for="(item, index) in items" :key="index" class="list-group-item">
        {{ item.nombre }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "MainComponent",
  props: {
    msg: String,
  },
  data() {
    return {
      items: []
    };
  },
  mounted() {
    // Realiza una llamada a la API al cargar el componente
    this.fetchItems();
  },
  methods: {
    fetchItems(){
        axios.get('http://127.0.0.1:8000/api/usuario').then((resp) => {
            console.log(resp.data);
            this.items = resp.data;
        }).catch((error) => {
          console.error("Error al obtener los datos:", error);
        });
    }
  }
};
</script>
