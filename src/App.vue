<template>
  <div id="app" >
    <h1>PIZZA</h1>
    <div v-if="loading" class="d-flex justify-content-center mb-3">
    loading...
    </div>
    <div v-if="!loading">
   <b-container>
    <b-row>
      <b-col xs="12" md="6" lg="4" v-for="(p,index) in pizzaArray" :key="index">
    <div>
      <b-card  
        
        img-src=".assets/pizza1.jpg"
        img-alt=""
        img-top
        tag="article"
        style="max-width: 20rem;"
        class="mb-2"
      >
        <h4 class="title"><b>{{ p.attributes.name.toUpperCase() }}</b></h4>
        <b-card-text>
        {{ p.attributes.description }}
        </b-card-text>
        <hr/>
        <div>
        <b-button
          :class="showCollapse ? 'collapsed' : null"
          :aria-expanded="showCollapse ? 'true' : 'false'"
          aria-controls="collapse-4"
          @click="showCollapse = !showCollapse"
          variant="danger">
        Toppings
          <b-badge variant="light">{{ p.attributes.toppings.length }}</b-badge>
        </b-button>
        <b-collapse id="collapse-4" v-model="showCollapse" class="mt-2">
          <b-badge pill variant="warning" my-3 v-for="(topping,index) in p.attributes.toppings" :key="index">
            {{ topping }}
          </b-badge>
        </b-collapse>
        </div>
        
        <div>
       </div>
       </b-card>
        </div>
        </b-col>
        
      </b-row>
    </b-container>
      
    </div>    
  </div>
</template>

<script>
import axios from 'axios';




export default{
  name: 'app',
  data () {
    return {
      pizzaArray: [],
      loading: false,
      showCollapse: true
    }
  },
  mounted () {
    this.loading = true
    axios
      .get('https://pizza.jptreen.com/api/pizzas')
      .then(response =>
      this.pizzaArray = response.data.data)
      this.loading = false
      
  }
  
}
</script>

<style  scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.badge-warning {
    color: #212529;
    background-color: #ffc107;
    margin: 3px 4px;
    font-size: 14px;
}
p {
    margin-top: 0;
    margin-bottom: 1rem;
    font-family: nexa light;
}
.title{
  color:rgb(1, 30, 155);
}
.card-body {
    -ms-flex: 1 1 auto;
    -webkit-box-flex: 1;
    flex: 1 1 auto;
    padding: 1.25rem;
    
    border-top: none;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    box-shadow: 0px 2px 0px 0px rgb(160, 160, 160);
}
.card-img-top {
    width: 100%;
    border-top-left-radius: calc(0.25rem - 1px);
    
    
}
img{
  background-image: url("./assets/pizza1.jpg");
  width: 700px;
  height: 300px;
  background-repeat: no-repeat;
  background-position: center;
  background-origin: content-box;
  cursor: pointer;
  
   
}

</style>
