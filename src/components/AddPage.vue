<script>
export default {
    data() {
        return {
            title: "",
            image: "",
            difficulty: "",
            duration: "",
            description: "",
            ingredients: [],
        }
    },
    methods: {
        addIngredient() {
            this.ingredients.push({ ingName: "", ingWeight: "" })
            console.log(this.ingredients)
        },
        removeIngredient(item) {
            let index = this.ingredients.indexOf(item)
            this.ingredients.splice(index, 1)
        },
        showProperties() {
            let tempTitle = this.title
            let tempImg = this.image
            let tempDiff = this.difficulty
            let tempTime = this.duration
            let tempDesc = this.description

            const values = this.ingredients.map((el) => ({
                ingName: el.ingName,
                ingWeight: el.ingWeight,
            }))
            if (
                tempTitle != "" &&
                tempDiff != "" &&
                tempTime != "" &&
                values.length != 0
            ) {
                values.forEach((el) => {
                    if (el.ingName == "" || el.ingWeight == "") {
                        return
                    }
                })
                let RecipeStorage = []
                const storedData = localStorage.getItem("przepisy")
                let obj = {
                    title: tempTitle,
                    image: tempImg,
                    difficulty: tempDiff,
                    duration: tempTime,
                    description: tempDesc,
                    ingredients: values,
                }

                if (storedData) {
                    RecipeStorage = JSON.parse(storedData)
                }

                RecipeStorage.push(obj)

                localStorage.setItem("przepisy", JSON.stringify(RecipeStorage))
            }
        },
    },
}
</script>
<script setup>
import ProductItem from "./ProductItem.vue"
</script>
<template>
    <div class="AddForm">
        <section class="FormPanel">
            <div class="left">
                <label for="addTitle">Tytuł</label>
                <input
                    type="text"
                    id="addTitle"
                    v-model="title"
                    placeholder="dodaj tytuł"
                />
                <label for="addImg">Zdjęcie</label>
                <input
                    type="text"
                    id="addImg"
                    placeholder="(link)"
                    v-model="image"
                />
                <label for="addDiff">Poziom trudności</label>
                <select
                    id="addDiff"
                    v-model="difficulty"
                >
                    <option
                        disabled
                        hidden
                        value=""
                    >
                        Wybierz poziom trudności
                    </option>
                    <option value="Łatwy">Łatwy</option>
                    <option value="Średni">Średni</option>
                    <option value="Trudny">Trudny</option>
                </select>
                <label for="addTime">Czas trwania: </label>
                <input
                    type="text"
                    id="addTime"
                    placeholder="(min)"
                    v-model="duration"
                />
                <label for="addDesc">Opis</label>
                <textarea
                    id="addDesc"
                    cols="30"
                    rows="9"
                    v-model="description"
                    placeholder="Dodaj opis np. proces przygotowania"
                ></textarea>
            </div>
            <div class="right">
                <!-- <label for="">Podgląd zdjęcia</label>
                <div class="imageView">
                    <img
                        :src="image"
                        alt="podgląd zdjęcia"
                    />
                </div> -->

                <div class="ingredients">
                    <label
                        for=""
                        class="en"
                        >Składniki</label
                    >
                    <box-icon
                        name="plus"
                        class="plus"
                        @click="addIngredient"
                    ></box-icon>
                </div>
                <div class="ingredientBox">
                    <!-- <ProductItem /> -->
                    <p v-if="ingredients.length === 0">Nie dodano składników</p>
                    <div
                        class="wrapp"
                        v-for="item in ingredients"
                    >
                        <input
                            type="text"
                            id="ingName"
                            placeholder="Nazwa produktu"
                            v-model="item.ingName"
                        />
                        <input
                            type="text"
                            id="ingWeight"
                            placeholder="waga produktu (g)"
                            v-model="item.ingWeight"
                        />
                        <box-icon
                            name="trash"
                            @click="removeIngredient(item)"
                            animation="tada-hover"
                        ></box-icon>
                        <!-- -->
                    </div>
                </div>
                <button
                    class="showProp"
                    @click="showProperties"
                >
                    Dodaj przepis
                </button>
            </div>
        </section>
    </div>
</template>

<style scoped>
.AddForm * {
    display: block;
}
.FormPanel {
    background-color: white;
    padding: 20px;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
}
.ingredients {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
}
.ingredientBox {
    width: 600px;
    display: flex;
    flex-direction: column;
    overflow-y: scroll;
    height: 350px;
    border-top: 1px solid #d9e1fc;
}
.wrapp {
    display: flex;
    flex-direction: row;
    border: 2px solid #d9e1fc;
    border-radius: 5px;
    background-color: aliceblue;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
}
input[type="text"] {
    border: 2px solid #d9e1fc;
    border-radius: 5px;
    padding: 10px;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
}
.imageView {
    width: 400px;
}
.imageView img {
    width: 400px;
    border: 3px dashed #d9e1fc;
    min-height: 200px;
    text-align: center;
    margin: 0px;
}
.right {
    display: flex;
    /* justify-content: center; */
    flex-direction: column;
    align-items: left;
}
.showProp {
    width: 300px;
    padding: 20px;
    background-color: white;
    border: 2px solid #d9e1fc;
    border-radius: 10px;
    font-size: 20px;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
}
.showProp:hover {
    background-color: aliceblue;
}
#addDiff,
#addDesc {
    padding: 10px;
    border: 2px solid #d9e1fc;
    border-radius: 5px;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
    resize: none;
}
</style>
