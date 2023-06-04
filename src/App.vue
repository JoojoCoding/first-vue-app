<script setup>
import { RouterLink, RouterView } from "vue-router"
import HelloWorld from "./components/HelloWorld.vue"
import LogoTemp from "./components/LogoTemp.vue"
//import "./App.css"

</script>

<template>
    <div class="wrapper">
      <LogoTemp /> 
        <div class="content">
            <nav class="navbar">
                <ul>
                    <li>
                        <RouterLink to="/">Strona Główna</RouterLink>
                    </li>
                    <li>
                        <RouterLink to="/favorite">Ulubione</RouterLink>
                    </li>
                    <li><RouterLink to="/add-recipe">Dodaj Przepis</RouterLink></li>
                </ul>
            </nav>
            <RouterView class="View"/>
        </div>
    </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
*{
    font-family: 'Montserrat', sans-serif;
    
}
*::-webkit-scrollbar {
    width: 16px;
  }

  *::-webkit-scrollbar-track {
    background: rgba(red, green, blue, 0);
  }

  *::-webkit-scrollbar-thumb {
    background-color: #d9e1fc;
    border-radius: 10px;
    /* border: 3px solid #ffffff; */
  }
body{
    background-color: aliceblue;
}
.wrapper{
    /* border: 2px solid black; */
    border-radius: 5px;
    padding: 10px;
}
.content{
    display: flex;
    flex-direction: row;
    align-items: top;
    justify-content: flex-start;
}
.content *{
    margin: 20px;
}
.navbar{
   
    border-radius: 5px;
    position: sticky;
    padding: 10px;
    width: 30vw;
    height: 80vh;
    background-color: white;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
}

.navbar ul{
    text-align: left;
    display: flex;
    flex-direction: column;
    padding: 0;
    background-color: inherit;
}
.navbar ul li{
    list-style-type: none;
    display: block;
    font-size: 30px;
    padding: 10px;
    background-color: inherit;
}
.navbar ul li:hover{
    background-color: aliceblue;
    border-radius: 5px;
    padding: 10px;
}
.navbar ul li *{
    text-decoration: none;
    color: black;
    background-color: inherit;
}
.navbar ul li *:active{
    color: dodgerblue;
}
.View{
    overflow-y: scroll;
    height: 80vh;
    width: 80vw;
}
</style>
