<template>
  <v-autocomplete
    v-model="model"
    :items="items"
    :loading="isLoading"
    :search-input.sync="search"
    background-color="grey lighten-3"
    rounded
    clearable
    hide-no-data
    hide-selected
    placeholder="Ciudad"
    item-text="Description"
    item-value="API"
    return-object />
</template>

<script>
  import config from '../../config'

  export default {
    data: () => ({
      descriptionLimit: 60,
      entries: [],
      isLoading: false,
      model: null,
      search: null,
    }),

    computed: {
      fields () {
        if (!this.model) return []

        return Object.keys(this.model).map(key => {
          return {
            key,
            value: this.model[key] || 'n/a',
          }
        })
      },
      items () {
        return this.entries.map(entry => (
           Object.assign({}, {Description : entry.place_name,  value: entry.center}) 
          ))
      },
    },

    watch: {
      model (val){
        if(val === undefined) return
        this.$emit('modelChanged', val)
      },
      search (val) {
        if (this.search === null || this.search === '' || this.search === undefined) return
        if (this.isLoading) return
        this.isLoading = true
        fetch(`${config.geocoderApi}/${val}`)
          .then(res => res.json())
          .then(res => {
            this.entries = res
          })
          .catch(err => {
            console.log(err)
          })
          .finally(() => (this.isLoading = false))
      },
    },
  }
</script>