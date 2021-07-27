<template>
    <section id="show">
        <article id="error">{{ errorMessage }}</article>
        <p v-for="(good,i) in pickedGoods" :key="i" @click="$emit('delete-picked-good',good)">{{ good }}</p>
    </section>
</template>

<script>
export default {
    name: "ShowGoods",
    props: ["pickedGoods", "errorMessage"],
    emits: ['delete-picked-good']
};
</script>

<style scoped>
#user #show {
    overflow-y: scroll;
    height: 231px;
    padding-top: 55px;
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
    justify-content: flex-start;
}

#show p {
    display: inline-block;
    margin: 2px;
    background-color: #ff7700;
    padding: 5px;
    color: white;
    font-size: 1.1em;
    position: relative;
}

#show p:hover {
    cursor: pointer;
}

#show p:hover::before {
    display: block;
    content: '';
    transform: rotate(45deg);
    height: 100%;
    left: 50%;
    top: 0;
    background-color: #281aff;
    width: 2px;
    position: absolute;
}

#show p:hover::after {
    display: block;
    content: '';
    transform: rotate(-45deg);
    height: 100%;
    left: 50%;
    top: 0;
    background-color: #281aff;
    width: 2px;
    position: absolute;
}

#show #error {
    position: absolute;
    display: block;
    top: 10px;
    background: none;
    color: #4b55ff;
    font-weight: bold;
    font-size: 1.5em;
}

</style>
