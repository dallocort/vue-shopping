<template>
    <section id="removeGoods">
        <PickGoods :arrayGroup="arrayGroup"
                   :blocked="true"
                   @selected-group="selectedGroup=$event"></PickGoods>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <br/>
        <template v-if="selectedGroup">
            <p v-for="(good,i) in arrayGoods.filter(el=>el.group===selectedGroup)"
               :key="i"
               @click="$emit('remove-goods',good)">
                <span style="color:darkgreen">{{ `(${good.group})` }} -</span>
                {{ good.name }}
                <button @click="$emit('remove-goods',good.value)">DELETE
                                                                  {{ good.name
                                                                  }}
                </button>
            </p>
        </template>
        <p v-else>SELECT GROUP OF GOODS!</p>
    </section>
</template>

<script>
import PickGoods from "@/components/PickGoods.vue";

export default {
    name: "RemoveGoods",
    components: {PickGoods},
    props: ['arrayGroup', 'arrayGoods'],
    emits: ['remove-goods'],
    data() {
        return {
            errorMessage: '', buttonLabel: '', selectedGroup: ''
        };
    },
    watch: {}
};
</script>

<style scoped>
#removeGoods {
    float: left;
    width: 70%;
    text-align: center;
    padding: 0 20px 20px;
}

#removeGoods #pick {
    padding-top: 6px;
}

#removeGoods button {
    margin: 4px;
    height: 25px;
    /* font-weight: bold; */
    background-color: #318c49;
    border: 1px solid #318c49;
    color: white;
}

#removeGoods p {
    color: #b1edff;
    font-weight: bold;
}

#removeGoods button:active {
    background-color: #4c4a40;
    color: white;
}
</style>
