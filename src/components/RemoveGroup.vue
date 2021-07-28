<template>
    <section id="removeGroup">
        <PickGoods :arrayGroup="arrayGroup"
                   :blocked="true"
                   @selected-group="selectedGroup=$event"></PickGoods>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <br/>
        <button v-if="buttonLabel" type="button" @click="removeGroup">
            {{ buttonLabel }}
        </button>
        <p v-else>SELECT GROUP OF GOODS!</p>
    </section>
</template>

<script>
import PickGoods from "@/components/PickGoods.vue";

export default {
    name: "RemoveGroup",
    components: {PickGoods},
    props: ['arrayGroup', 'arrayGoods'],
    emits: ['remove-group'],
    data() {
        return {
            errorMessage: '', buttonLabel: '', selectedGroup: ''
        };
    },
    methods: {
        removeGroup() {
            if (this.arrayGoods.find(
                el => el.group === this.selectedGroup) === undefined) {
                this.$emit('remove-group', this.selectedGroup);
                this.errorMessage = '';
                this.buttonLabel = '';
            } else {
                this.errorMessage = `GROUP "${this.selectedGroup}" HAS GOODS INSIDE, SO CAN NOT BE REMOVED!`;
            }
        }
    },
    watch: {
        selectedGroup(newValue) {
            this.buttonLabel = `REMOVE GROUP: ${newValue}`;
        }
    }
};
</script>

<style scoped>
#removeGroup {
    float: left;
    width: 70%;
    text-align: center;
    padding: 0 20px 20px;
}

#removeGroup #pick {
    padding-top: 6px;
}

#removeGroup button {
    margin: 10px;
    height: 39px;
    font-weight: bold;
    background-color: orange;
    border: 1px solid #a52f00;
}

#removeGroup button:active {
    background-color: #5f5c4f;
    color: white;
}
</style>
