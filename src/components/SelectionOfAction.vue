<template>
    <section id="radioButtons">
        <input id="choice1"
               v-model="selectedRadio"
               name="izbor"
               type="radio"
               value="newGroup">
        <label for="choice1">ADD NEW GROUP</label>
        <br/>
        <input id="choice2"
               v-model="selectedRadio"
               name="izbor"
               type="radio"
               value="newGoods">
        <label for="choice2">ADD NEW GOODS</label>
        <br/>
        <input id="choice3"
               v-model="selectedRadio"
               name="izbor"
               type="radio"
               value="removeGroup">
        <label for="choice3">REMOVE GROUP</label>
        <br/>
        <input id="choice4"
               v-model="selectedRadio"
               name="izbor"
               type="radio"
               value="removeGoods">
        <label for="choice4">REMOVE GOODS</label>
    </section>
</template>

<script>
export default {
    name: "SelectionOfAction",
    emits: ['select-radio'],
    data() {
        return {
            selectedRadio: ''
        };
    },
    watch: {
        selectedRadio(newValue) {
            this.$emit('select-radio', newValue);
        }
    }
};
</script>

<style scoped>
#radioButtons {
    padding: 20px;
    float: left;
    width: 30%;
}

#radioButtons label, #radioButtons input {
    display: inline-block;
}

#radioButtons input {
    margin: 0 10px 10px 0;
    display: inline-block;
    font-size: 1.1em;
}

</style>
