<script>
   // import "../assets/LogoTemp.css"
</script>
<template>
    <header>
        <h2>RecipeHub</h2>
        <h2>Wojciech Bernat</h2>
    </header>
</template>

<style scoped>
header{
    border: white;
    background-color: white;
    color: black;
    display: flex;
    flex-direction: row;
    box-shadow: 2px 1px 30px -17px rgba(66, 68, 90, 1);
}
header *{
    align-content: center;
    background-color: white;
}
header h2:first-child{
    position: relative;
    left: 5%;
}
header h2:last-child{
    position: absolute;
    right: 5%;
}
</style>