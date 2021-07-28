<template>
    <section id="newGoods">
        <PickGoods :arrayGroup="arrayGroup"
                   :blocked="true"
                   @selected-group="selectedGroup=$event"></PickGoods>
        <label for="good">Enter Good to add:</label>
        <input id="good"
               v-model.trim="newGoodToAdd"
               type="text"
               @keydown.enter="addNewGood"/>
        <br/>
        <button v-if="buttonLabel" type="button" @click="addNewGood">
            {{ buttonLabel }}
        </button>
        <p v-else>SELECT GROUP OF GOODS!</p>
        <article v-if="errorMessage">{{ errorMessage }}</article>
    </section>
</template>

<script>
import PickGoods from "@/components/PickGoods.vue";

export default {
    name: "NewGoods",
    components: {PickGoods},
    props: ['arrayGroup', 'arrayGoods'],
    emits: ['add-new-good'],
    data() {
        return {
            selectedGroup: '',
            newGoodToAdd: '',
            buttonLabel: '',
            errorMessage: ''
        };
    },
    methods: {
        addNewGood() {
            if (this.validate()) {
                this.errorMessage = `GOOD NAME "${this.newGoodToAdd.toLowerCase()}" IS NOT AVAILABLE!`;
            } else {
                this.$emit('add-new-good', {
                    group: this.selectedGroup.toLowerCase(),
                    value: this.newGoodToAdd.toLowerCase(),
                    name: this.newGoodToAdd.toLowerCase()
                });
                this.errorMessage = '';
            }
            this.newGoodToAdd = '';
        }, validate() {
            return this.newGoodToAdd === '' || this.arrayGoods.find(
                el => el.value === this.newGoodToAdd.toLowerCase()) !== undefined || this.arrayGoods.find(
                el => el.group === this.newGoodToAdd.toLowerCase()) !== undefined || this.arrayGoods.find(
                el => el.name === this.newGoodToAdd.toLowerCase()) !== undefined || this.arrayGroup.find(
                el => el.name === this.newGoodToAdd.toLowerCase()) !== undefined || this.arrayGroup.find(
                el => el.value === this.newGoodToAdd.toLowerCase()) !== undefined;
        }
    },
    watch: {
        selectedGroup(newValue) {
            this.buttonLabel = `ADD TO GROUP: ${newValue}`;
        }
    }
};
</script>

<style scoped>
#newGoods {
    float: left;
    width: 70%;
    text-align: center;
    padding: 0 20px 30px;
}

#newGoods #pick {
    padding-top: 6px
}

#newGoods button {
    margin: 10px;
    height: 39px;
    font-weight: bold;
    background-color: orange;
    border: 1px solid #a52f00;
}

#newGoods button:active {
    background-color: #5f5c4f;
    color: white;
}

#newGoods input {
    height: 30px;
    font-size: 1.1em;
}

#newGoods label {
    display: block;
    margin-bottom: 6px;
    font-size: 1.1em;
}

#newGoods p {
    margin-top: 16px;
    font-size: 1.1em;
}

</style>
