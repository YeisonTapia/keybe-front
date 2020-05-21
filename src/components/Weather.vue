<template>
  <div>
    <v-row
      align="center"
      justify="center" >
      <v-col
        cols="12"
        sm="12"
        md="12" >
        <SearcCountry @modelChanged="handlerModelChanged"/>
        <v-row
          align="center"
          justify="center" >

          <Forecast 
            :showArrows="false"
            title="Ahora mismo"
            v-if="currently" 
            :items="[currently]" />

          <Forecast 
            title="Esta Hora"
            v-if="hourly" 
            :items="hourly.data" />

          <Forecast 
            title="Esta Semana"
            v-if="daily" 
            :items="daily.data" />

        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import SearcCountry from '../components/SearchCountry';
import Forecast from '../components/Forecast'
export default {
  components:{
    SearcCountry,
    Forecast
  },
  data(){
    return{
      isLoading: false,
      currently: null,
      hourly: null,
      daily:null
    }
  },
  methods:{
    handlerModelChanged(event){
      if(event === '' || event.value === undefined) {
        this.currently = null
        this.hourly = null
        this.daily = null
        return
      }
      this.searchWeather(event.value[1], event.value[0])
    },
    searchWeather(lat, lng){
      this.isLoading = true
      fetch(`http://localhost:3000/api/weather/${lat}/${lng}`)
        .then(res => res.json())
        .then(res => {
          const {currently, hourly,daily} = res
          this.currently = currently
          this.hourly = hourly
          this.daily = daily
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => (this.isLoading = false))
    }
  }

}
</script>
