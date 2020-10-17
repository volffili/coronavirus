<template>
<div id="app">
  <main>

    <div class="wrap">
        <div class="title">Česko COVID-19</div>
        <div class="subtitle">Podíl hospitalizovaných</div>
        <div class="box">
          <div class="cases">3%</div>
        </div>
    </div>

  </main>
</div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
        api_key: 'v8Man2nWdPrvySsbuWiq2AkAB'
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
  font-size: 32px;
  font-weight: 500;
  text-align:center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.wrap .subtitle{
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style:italic;
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
