<template>
  <div class="table-container">
    <div class="table-headers">
      <span class="table-content">Tienda</span>
      <span class="table-content">Paseantes</span>
      <span class="table-content">Visitas</span>
      <span class="table-content">Atracción</span>
      <span class="table-content">Tickets</span>
      <span class="table-content">Ticket Promedio</span>
      <span class="table-content">Articulos</span>
      <span class="table-content">Artículos x ticket</span>
      <span class="table-content">Permanencia Promedio</span>
      <span class="table-content">Días Apagados</span>
    </div>
    <div v-for="item in data" :key="item.id" class="table-data">
      <span class="table-content">{{item.title}}</span>
      <span class="table-content">{{item.peasantsTotal.toLocaleString()}}</span>
      <span class="table-content">{{item.visitorsTotal.toLocaleString()}}</span>
      <span class="table-content">{{item.atraction.toFixed(2)}}</span>
      <span class="table-content">{{item.ticketsTotal.toLocaleString()}}</span>
      <span class="table-content">{{item.averageTicket.toLocaleString()}}</span>
      <span class="table-content">{{item.totalItems.toLocaleString()}}</span>
      <span class="table-content">{{item.itemPerTicket.toLocaleString()}}</span>
      <span class="table-content">{{item.averagePermanence.toLocaleString()}}</span>
      <span class="table-content">{{item.daysOff}}</span>
    </div>
    <div class="table-data">
      <span class="table-content">Total</span>
      <span class="table-content">{{dataPeasantsTotal.toLocaleString()}}</span>
      <span class="table-content">{{dataVisitorsTotal.toLocaleString()}}</span>
      <span class="table-content">{{dataAtractionTotal.toLocaleString()}}</span>
      <span class="table-content">{{dataTicketsTotal.toLocaleString()}}</span>
      <span class="table-content">{{dataAverageTicketTotal.toLocaleString()}}</span>
      <span class="table-content">{{dataTotalItems.toLocaleString()}}</span>
      <span class="table-content">{{dataTotalItemPerTicket.toLocaleString()}}</span>
      <span class="table-content">{{dataTotalAveragePermanence.toLocaleString()}}</span>
      <span class="table-content">{{dataTotalDaysOff.toLocaleString()}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DataTable',
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  computed: {
    dataPeasantsTotal(){
      return this.data.reduce((sum, item) => {
        return sum + item.peasantsTotal
      }, 0)
    },
    dataVisitorsTotal(){
      return this.data.reduce((sum, item) => {
        return sum + item.visitorsTotal
      }, 0)
    },
    dataAtractionTotal(){
      return this.data.reduce((sum, item) => {
        return sum + item.atraction
      }, 0)
    },
    dataTicketsTotal(){
      return this.data.reduce((sum, item) => {
        return sum + item.ticketsTotal
      }, 0)
    },
    dataAverageTicketTotal(){
      return this.data.reduce((sum, item) => {
        return sum + item.averageTicket
      }, 0)
    },
    dataTotalItems(){
      return this.data.reduce((sum, item) => {
        return sum + item.totalItems
      }, 0)
    },
    dataTotalItemPerTicket(){
      return this.data.reduce((sum, item) => {
        return sum + item.itemPerTicket
      }, 0)
    },
    dataTotalAveragePermanence(){
      return this.data.reduce((sum, item) => {
        return sum + item.averagePermanence
      }, 0)
    },
    dataTotalDaysOff(){
      return this.data.reduce((sum, item) => {
        return sum + item.daysOff
      }, 0)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url(https://www.w3schools.com/w3css/4/w3.css);

.table-container{
  border: 1px solid green;
  box-shadow: 4px 7px 5px 0px rgba(157,201,166,1);
  width: 100%
}

.table-headers{
  background-color: #56AE7A;
  color: whitesmoke;
  display: flex;
  justify-content: space-around
}

.table-data{
  display: flex;
  justify-content: space-around
}

.table-content{
  padding: 1rem;
  display: flex;
  align-items: center;
  max-width: 7rem;
  justify-items: center
}
</style>
