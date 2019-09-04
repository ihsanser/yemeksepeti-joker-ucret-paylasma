<template>
  <v-container style="max-width:600px">
    <v-layout
      text-center
      wrap
    >
    <v-col cols="12" sm="12">
      <h1>Joker Sonrası Hesaplama Aracı</h1>
    </v-col>
    <v-col cols="12" sm="12">
      <p>Kişilerin joker öncesi tutarlarını giriniz:</p>
    </v-col>
    <v-row
      align="center"
      class="grey lighten-5"
      cols="12" sm="12"
      v-for="(name,index) in names"
    >
      <v-col cols="6" sm="6">
        <v-text-field
        v-model="before[index]"
        :label="name+' aldıkları toplam'"
        outlined
        :hide-details="true"
        ></v-text-field>
      </v-col>
      <v-col cols="6" sm="6">
        <p>Ödenecek: {{ calculate(index) }}</p>
      </v-col>
    </v-row>
    <hr style="width:120%">


    <v-row
      align="center"
      class="grey lighten-5"
    >
      <v-col cols="6" sm="6">
        <p :style="'color:'+ beforeSumColor">Toplam: {{ beforeSum() }}</p>
      </v-col>
      <v-col cols="6" sm="6">
        <p :style="'color:'+ afterSumColor">Toplam: {{ afterSum() }}</p>
      </v-col>
    </v-row>



    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    beforeTotal: null,
    afterTotal: null,
    names: [
      'İhsan', 'MKV', 'Emir', 'Nadide'
    ],
    before: [],
    after: []
  }),
  methods: {
    calculate(index) {
      for (let i=0;i<this.before.length;i++){
        this.after[i] = this.before[i]*this.afterPrice()/this.beforeSum()
      }
      if (this.after[index])
        return this.after[index]
      else
        return null
    },
    afterSum() {
      if (this.after.length>0)
        return this.after.reduce((a,b) => Number(a)+Number(b))
      else {
        return 0
      }
    },
    beforeSum() {
      if (this.before.length>0)
        return this.before.reduce((a,b) => Number(a)+Number(b))
      else
        return 0
    },
    afterPrice() {
      let as = this.beforeSum()
      if (as >= 120){
        return as-45
      }else if (as >= 70){
        return as-25
      }else if (as >= 40) {
        return as-15
      }else if (as >= 30) {
        return as-10
      }else {
        return as
      }
    }
  },
  computed: {

    beforeSumColor() {
      if (this.beforeSum == this.beforeTotal)
        return "green"
      else
        return "red"
    },
    afterSumColor() {
      if (this.afterSum == this.afterTotal)
        return "green"
      else
        return "red"
    }
  }
};
</script>

<style media="screen">
  hr {
    transform: translateX(-10%);
    width: "120%";
  }

  p {
    margin: 0 !important;
  }
</style>
