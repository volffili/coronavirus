<template>
<div id="app">
  <main>

    <div class="wrap" v-if="typeof cases != 'undefined'">
        <div class="title">
          <p>COVID-19 v České republice</p>
          <p>Statistika <b>aktuálně <u>nakažených</u> koronavirem</b></p>
        </div>
        <div class="subtitle">V kritickém stavu</div>
        <div class="box">
          <div class="cases">{{(cases.critical/cases.active*100).toFixed(1)}}%</div>
        </div>
        <div class="subtitle">Hospitalizovaných</div>
        <div class="box">
          <div class="cases">{{(cases.hospitalized/cases.active*100).toFixed(1)}}%</div>
        </div>
        <div class="subtitle">S věkem nad 65 let</div>
        <div class="box">
          <div class="cases">{{(this.older55*100).toFixed(1)}}%</div>
        </div>
    </div>

  </main>
</div>
</template>

<script>
export default {
  name: 'App',
  created (){
    this.fetchData();
    console.log(this.cases);
  },
  data(){
    return {
      url:  'https://api.apify.com/v2/key-value-stores/K373S4uCFR9W1K8ei/records/LATEST?disableRedirect=true',
      cases: {}
    }
  },
  methods: {
    fetchData(){
      fetch(this.url).then(res => res.json()).then(this.setResults); 
    },
    setResults(results){
      this.cases = results; 
      this.byAge = {};
      this.cases.infectedByAgeSex.forEach(({infectedByAge}) => {
        infectedByAge.forEach(({age,value})=>{
          if(age !== ""){
            this.byAge[age] = this.byAge[age] ? this.byAge[age]+value : value;
          }
        })
      })
      let total = 0;
      for(let age in this.byAge){
          total += this.byAge[age];
      }
      this.older55 = 0;
      for(let age in this.byAge){
          if(Number(age.substring(0,2)) >= 65){
            this.older55 += this.byAge[age] /= total;
          }
      }
    }
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}

body{
  font-family:'montserrat', sans-serif;   
}

#app{
  background-color:grey;
}

main{
  min-height: 100vh; 
  padding:25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25),rgb(0,0,0,0.75));
}

.wrap .title{
  color: white;
  padding:40px;
  font-size: 32px;
  font-weight: 500;
  text-align:center;
}

.wrap .subtitle{
  color: white;
  font-size: 20px;
  font-weight: 300;
  text-align:center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.box{
  text-align: center;  
}

.box .cases{
  display:inline-block;
  padding: 10px 25px;
  color:white;
  font-size:102px;
  font-weight:900;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color:rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
</style>
