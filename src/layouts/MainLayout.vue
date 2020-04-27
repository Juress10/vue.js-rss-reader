<template>
  <div class="q-pa-md">
    <q-toolbar class="bg-transparent text-black q-my-md row">
      <img src="~assets/logo--blue.png" alt="logo" class="logo-size">

      <q-space />
      <div class="row col-6">
        
        <q-input class="col-8" color="blue-grey-5" dense="dense" 
        style="max-width:600px; margin-right:5px;" 
        v-model="url">
          <template v-slot:prepend >
            <a v-on:click="changeUrl()" href="#" style="text-decoration:none">
              <q-icon 
              size="sm"
              name="refresh"
              color="blue-grey-5" 
              />
            </a>
          </template>
        </q-input>
        <q-btn flat class="col-2 fw-md blue-text" 
        v-on:click="changeUrl()" color="black" label="FETCH" />
      </div>

      <q-space />
      
      <q-btn-dropdown  flat class="col-1" label="Sort">
        <q-list>
          <q-item clickable v-close-popup tabindex="0">
            <q-item-section v-on:click="sortAsc()">
              <q-item-label style="font-size:0.8rem">ascending</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable v-close-popup tabindex="0">
            <q-item-section v-on:click="sortDesc()">
              <q-item-label style="font-size:0.8rem">descending</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
      <q-separator dark vertical />
     
    </q-toolbar>
    <router-view :url="url" ref="index"/>
    
  </div>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      url: 'https://www.sme.sk/rss-title',
      sortType: null
    }
  },
  methods : {
    changeUrl () {
      this.$refs.index.fetchByUrl()
    },
    sortDesc () {
      this.$refs.index.sortDesc()
    },
    sortAsc () {
      this.$refs.index.sortAsc()
    }
  }
}
</script>

<style scoped>
  .q-pa-md{
    padding:0px;
  }
  .q-mt-md, .q-my-md {
    margin-top: 0px;
  }
  .q-mb-md, .q-my-md {
    margin-bottom: 16px;
  }
  .logo-size{
    height:80px;
  }
  .q-field__control {
     color: rgb(120,144,156) !important;
  }
  .blue-text{
    color:rgb(34,58,92)!important;
  }
</style>
