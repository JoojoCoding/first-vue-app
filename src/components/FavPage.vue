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
                let favtab = []
                RecipeStorage.forEach(el => {
                    if(el.favorite){
                        favtab.push(el)
                    }
                })
                this.Recipes = favtab
                console.log(this.Recipes)
            }
        },  
    }
</script>
<template>
    <div class="FavPagePanel">
        <div class="recipeBoxes">
            <p v-if="Recipes.length === 0">Nie masz żadnych ulubionych przepisów</p>
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
            </div>
        </div>  
    </div>
</template>

<style>
.FavPagePanel {
    border-radius: 5px;
}

</style>