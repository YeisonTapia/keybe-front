<template>
    <v-col
      hide-on-leave="true"
      align="center"
      justify="center"
      cols="12"
      sm="12"
      md="12">
      <div class="title font-weight-bold" v-if="title">
        {{title}}
      </div>
      <div>
        <v-carousel hide-delimiters :show-arrows="showArrows" height="250"> 
          <v-carousel-item
            v-for="(item, i) in items"
            :key="i">
          <skycon  
            color="#e0e0e0"
            style="margin-top:50px"
            :condition="item.icon" 
            width="100" 
            height="100" />
            <div class="subtitle" >
              {{item.summary}}
            </div>
            <div class="subtitle" >
              {{  item.time | moment }}
            </div>
          </v-carousel-item>
        </v-carousel>
      </div>
    </v-col>
</template>

<script>
import moment from 'moment'

export default {
  props:{
    items:{
      type: Array,
      required: true,
      default: () => []
    },
    showArrows:{
      type: Boolean,      
      default: true
    },
    title:{
      type: String,
      required: false,
    }
  },
  filters: {
    moment: function (date) {
      moment.locale('es')
      return moment.unix(date).format("MMMM DD YYYY, h:mm:ss");
    }
  },
  mounted(){
    moment.locale('es')
  }
}
</script>
