<template>
    <section id="user">
        <PickGoods :arrayGoods="arrayGoods"
                   :arrayGroup="arrayGroup"
                   :blocked="blocked"
                   :pickedGoods="pickedGoods"
                   @error-message="$emit('error-message',$event)"
                   @add-to-picked-goods="$emit('add-to-picked-goods', $event);"></PickGoods>
        <ShowGoods :errorMessage="errorMessage"
                   :pickedGoods="pickedGoods"
                   @delete-picked-good="$emit('delete-picked-good',$event)"></ShowGoods>
    </section>

</template>

<script>
import PickGoods from "@/components/PickGoods.vue";
import ShowGoods from "@/components/ShowGoods.vue";

export default {
    name: "User",
    props: ['arrayGroup', 'arrayGoods', 'pickedGoods', "errorMessage"],
    emits: ['add-to-picked-goods', 'delete-picked-good', 'error-message'],
    components: {
        ShowGoods, PickGoods
    },
    data() {
        return {blocked: false};
    }
};
</script>

<style scoped>
#user {
    border-bottom: 1px solid #737373;
    background-color: #ead3ff;
}

#user::after {
    content: '';
    display: table;
    clear: both;
}

#user section:first-child {
    float: left;
    width: 40%;
    height: 100%;
}

#user section:last-child {
    float: left;
    width: 60%;
    height: 100%;
}
</style>
