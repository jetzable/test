<template>
  <DataTable v-if="!loading" :data="storesInfo" />
  <div v-else class="overlay">
    <span class="spinner"></span>
  </div>
</template>

<script>
// @ is an alias to /src
import DataTable from '@/components/DataTable.vue'


export default {
  name: 'DataTableView',
  components: {
    DataTable
  },
  data () {
    return {
      storesInfo: null,
      loading: false
    }
  },
  created () {
    this.getData()
  },
  methods: {
    async getData() {
      this.loading = true
      const stores = await require('../../brandDateData.json')
      const {data} = await require('../../assignedStore.json')
     
      this.storesInfo = stores.map(store => {
       const storeName = data.find(data => {
         return store.identifier === data.identifier
       })        
        const peasantsSum = Object.entries(store.peasants).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const visitorsSum = Object.entries(store.visitors).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const ticketsSum = Object.entries(store.tickets).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const revenueSum = Object.entries(store.revenue).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const itemsSum = Object.entries(store.items).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const permanenceSum = Object.entries(store.permanence).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const permanenceCountSum = Object.entries(store.permanenceCount).reduce((sum, entry) => {
          return sum + entry[1]
        }, 0)
        const daysOff = Object.entries(store.uptime).filter(entry => {
          return entry[1] === 0
        })
        return {
          id: store.identifier,
          peasantsTotal: peasantsSum,
          visitorsTotal: visitorsSum,
          atraction: (visitorsSum / peasantsSum) * 100,
          ticketsTotal: ticketsSum,
          persiasion: ticketsSum / visitorsSum,
          totalRevenue: revenueSum,
          averageTicket: revenueSum / ticketsSum,
          totalItems: itemsSum,
          itemPerTicket: (itemsSum / ticketsSum) / 100,
          averagePermanence: ((permanenceSum *100)/permanenceCountSum) / 6000000,
          daysOff: daysOff.length,
          title: storeName.name
        }        
      })
      this.loading = false
    }
  }
}
</script>
<style scoped>
.overlay {
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    position: fixed;
    background: #222;
    display: flex;
    flex-grow: 1;
    justify-content: center;
    align-items: center;
}

.spinner {
    width: 75px;
    height: 75px;
    display: inline-block;
    border-width: 2px;
    border-color: rgba(255, 255, 255, 0.05);
    border-top-color: #6AD074;
    animation: spin 1s infinite linear;
    border-radius: 100%;
    border-style: solid;
}

@keyframes spin {
  100% {
    transform: rotate(360deg);
  }
}
</style>