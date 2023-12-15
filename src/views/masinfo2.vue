<script>
import axios from 'axios';
import DataTable from "primevue/datatable";
import Column from "primevue/column";
import MiButton from 'primevue/button';
import InlineMessage from 'primevue/inlinemessage';
export default {
  components: {
    DataTable,
    Column,
    MiButton,
    InlineMessage,
  },
  data() {
    return {
      planetas2: [],
    };
  },
  mounted() {
    const savedPlanetas2 = localStorage.getItem('planetas2');

    if (savedPlanetas2) {
      this.planetas2 = JSON.parse(savedPlanetas2);
    } else {
      this.fetchPlanetas2();
    }
  },
  methods: {
    fetchPlanetas2() {
      axios
          .get('https://api.nasa.gov/planetary/apod?api_key=mBZ5Hr3Glv3ZkdE3xApJVbUoRKJF8MaOkG7UAdPt&count=10')
          .then(response => {
            this.planetas2 = response.data;
            localStorage.setItem('planetas2', JSON.stringify(this.planetas2));
          })
          .catch(error => {
            console.error('Error al obtener datos:', error);
          });
    },
    zoomImage(event) {
      event.target.style.transform = 'scale(1.5)';
      event.target.style.transition = 'transform 0.3s ease';
    },
    resetZoom(event) {
      event.target.style.transform = 'scale(1)';
    },
  },
};
</script>

<template>
  <main>
    <MiButton icon="pi pi-reddit">
      <RouterLink to="/Pagina2">Atrás</RouterLink>
    </MiButton>
    <DataTable :value="planetas2" class="custom-table">
      <Column field="title" header="Titulo"></Column>
      <Column header="Imagen">
        <template #body="planeta">
          <div class="custom-image-cell">
            <a :href="planeta.data.url" target="_blank">
              <img
                  :src="`${planeta.data.url}`"
                  alt=""
                  class="custom-image"
                  @mouseover="zoomImage"
                  @mouseleave="resetZoom"
              />
            </a>
          </div>
        </template>
      </Column>
      <Column field="explanation" header="Explicacion"></Column>
    </DataTable>
  </main>
  <InlineMessage severity="info">Creado por Dario Rata para Proyecto de Interfaces</InlineMessage>
</template>


<style>
/* Estilos para el DataTable */
.p-datatable table {
  border-collapse: collapse;
  width: 100%;
  border: 1px solid #d0d0d0;
  margin-bottom: 20px;
  overflow-x: auto;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;

}

.p-datatable th,
.p-datatable td {
  border: 1px solid #ccc;
  padding: 12px;
  text-align: left;
  transition: background-color 0.3s ease;

}

.p-datatable th {
  background-color: #f2f2f2;
  font-weight: bold;
}

.custom-image-cell {
  display: flex;
  align-items: center;
}

.custom-image {
  width: 100px;
  height: auto;
  margin-right: 50px;
  border-radius: 5px;
  transition: transform 0.3s ease;
}

.pi-search {
  margin-left: 5px;
  font-size: 16px;
  color: #008000;
}
.pi-refresh{
  float: right;
  font-size: 20px;
  color: #008000;
}


.p-datatable tbody tr:hover td {
  background-color: #d4edda;
  transition: background-color 0.3s ease;
  font-size: 20px;
  font-weight: bold;
}
</style>
