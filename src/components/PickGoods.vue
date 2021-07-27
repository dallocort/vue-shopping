<template>
    <section id="pick">
        <select id="group" v-model="selectedGroup" name="group">
            <option disabled hidden value="none">select group:</option>
            <option v-for="(group,i) in arrayGroup" :key="i" :value="group.value">{{ group.name }}</option>
        </select>
        <select v-if="selectedGroup!=='none' && blocked===false && arrayGoods.find(el=>el.group===selectedGroup) !==undefined "
                id="goods"
                v-model="selectedGood"
                name="goods"
                size="5">
            <option v-for="(good,i) in arrayGoods.filter(el=>el.group===selectedGroup)" :key="i" :value="good.value">
                {{ good.name }}
            </option>
        </select>
    </section>
</template>

<script>
export default {
    name: "PickGoods",
    props: {
        arrayGroup: Array,
        arrayGoods: Array,
        pickedGoods: Array,
        blocked: Boolean
    },
    emits: ['add-to-picked-goods', 'error-message', 'selected-group'],
    data() {
        return {
            selectedGood: '',
            selectedGroup: 'none'
        };
    },
    methods: {},
    watch: {
        selectedGroup(newValue) {
            if (this.blocked) {
                this.$emit('selected-group', newValue);
            }
        },
        selectedGood(newValue) {
            if (!this.blocked) {
                if (this.pickedGoods.find((el) => el === newValue) !== undefined) {
                    this.$emit('error-message', `you already picked ${newValue}!`);
                } else {
                    this.$emit('error-message', '');
                    this.$emit('add-to-picked-goods', newValue);
                }
            }
        }
    }
};
</script>

<style scoped>
#pick {
    padding: 20px;
}

#pick label {
    display: block;
    text-align: center;
    font-size: 1.1em;
}

select {
    margin: 15px auto 10px;
    display: block;
}

#group {
    height: 30px;
    background-color: #b1edff;
    font-size: 1em;
}

#goods option:checked {
}

#goods {
    background-color: #ffe3ad;
    font-size: 1em;
    padding: 5px;
}

</style>
