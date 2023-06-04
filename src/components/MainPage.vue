<script>
    export default {
        data(){
            return {
                Recipes: []
            }
        },
        mounted(){
            const storedData = localStorage.getItem("przepisy")
            let RecipeStorage = []
            console.log("mountyd")
            console.log(JSON.parse(storedData))
            if(storedData){
                RecipeStorage = JSON.parse(storedData)
                this.Recipes = RecipeStorage
                console.log(this.Recipes)
            }
        },  
        methods: {
            addToFavorite(box){    
                box.favorite = true
                console.log(box)
                localStorage.setItem("przepisy", JSON.stringify(this.Recipes))
            },
            removeFavorite(box){
                box.favorite = false
                console.log(box)
                localStorage.setItem("przepisy", JSON.stringify(this.Recipes))
            }
        }
    }
</script>
<template>
    <div class="MainPagePanel">
        <!-- <input type="text" name="" id="" />
        <button>szukaj</button> -->
        <div class="recipeBoxes" >
            <p v-if="Recipes.length === 0">Nie znaleziono przepisów</p>
            <div class="box" v-for="box in Recipes">
                <img :src="box.image" alt="zdjęcie" class="boxImg">
                <div class="boxContent">
                    <h1>{{ box.title }}</h1>
                    <p>Poziom trudności: &nbsp;{{ box.difficulty }}</p>
                    <p>Czas wykonania: &nbsp;{{ box.duration }}min</p>
                    <p>Opis</p>
                    <p>{{ box.description }}</p>
                    <div class="inglist">
                        <p>Składniki: </p>
                        <p>
                            <span v-for="ing in box.ingredients">{{ ing.ingName }} {{ ing.ingWeight}}g, </span>
                        </p>
                    </div>
                </div>
                <box-icon name='heart' @click="addToFavorite(box)" class="heart" size="lg" v-if="!box.favorite" animation="tada-hover"/>
                <box-icon name='heart' @click="removeFavorite(box)" class="heart" size="lg" v-if="box.favorite" type="solid" color="crimson" animation="flashing-hover"/>
            </div>
        <!-- <div class="recipeBoxes">
            
            <div class="box"></div>
            <div class="box"></div> -->
            
        </div>
    </div>
</template>
<style>
.MainPagePanel {
   
    border-radius: 5px;
}
.recipeBoxes{
    /* display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-evenly; */
    display: grid;
    gap: 30px;
    grid-template-columns: 1fr ;
}
.box{
    /* width: 500px; */
    
    background-color: white;
    border-radius: 5px;
    margin: 10px;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
    display: flex;
    flex-direction: row;
}
.boxImg{
    width: 50%;
    
    border-radius: 5px;
}
.heart{
    width: 50px;
    /* position: relative;
    left: 12%;
    top: 2%; */

}
.inglist {
    display: inline-block;
    text-align: left;
    padding: 0px;
}
.inglist *{
    margin: 0px;
}
</style>
