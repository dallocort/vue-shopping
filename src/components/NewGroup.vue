<template>
    <section id="newGroup">
        <label for="addNewGroup"></label>
        <input id="addNewGroup" v-model.trim="newGroupValue" type="text" @keydown.enter="addNewGroup"/>
        <button @click="addNewGroup">ADD NEW GROUP</button>
        <article>{{ errorMessage }}</article>
    </section>
</template>

<script>
export default {
    name: "NewGroup",
    props: ['arrayGroup', 'arrayGoods'],
    emits: ['add-new-group'],
    data() {
        return {
            errorMessage: '',
            newGroupValue: ''
        };
    },
    methods: {
        addNewGroup() {
            if (this.validate()) {
                this.errorMessage = `GROUP NAME "${this.newGroupValue.toLowerCase()}" IS NOT AVAILABLE!`;
                this.newGroupValue = '';
            } else {
                this.$emit('add-new-group', this.newGroupValue.toLowerCase());
                this.errorMessage = '';
                this.newGroupValue = '';
            }
        },
        validate() {
            return this.newGroupValue === '' || this.arrayGoods.find(el => el.value === this.newGroupValue.toLowerCase()) !== undefined || this.arrayGoods.find(el => el.group === this.newGroupValue.toLowerCase()) !== undefined || this.arrayGoods.find(el => el.name === this.newGroupValue.toLowerCase()) !== undefined || this.arrayGroup.find(el => el.name === this.newGroupValue.toLowerCase()) !== undefined || this.arrayGroup.find(el => el.value === this.newGroupValue.toLowerCase()) !== undefined;
        }
    }
};
</script>

<style scoped>
#newGroup {
    float: left;
    width: 70%;
    text-align: center;
    padding: 20px;
}

#newGroup button {
    display: inline-block;
    margin-left: 5px;
}

#newGroup article {
    margin-top: 20px;
    color: #a90101;
    font-size: 1.1em;
}
</style>
