<template>
    <section id="admin">
        <SelectionOfAction @select-radio="selectedRadio=$event"></SelectionOfAction>
        <NewGroup v-if="selectedRadio==='newGroup'"
                  :arrayGoods="arrayGoods"
                  :arrayGroup="arrayGroup"
                  @add-new-group="$emit('add-new-group',$event)"></NewGroup>
        <NewGoods v-else-if="selectedRadio==='newGoods'"
                  :arrayGoods="arrayGoods"
                  :arrayGroup="arrayGroup"
                  @add-new-good="$emit('add-new-good',$event)"></NewGoods>
        <RemoveGroup v-else-if="selectedRadio==='removeGroup' "
                     :arrayGoods="arrayGoods"
                     :arrayGroup="arrayGroup"
                     @remove-group="$emit('remove-group',$event)"></RemoveGroup>
        <RemoveGoods v-else-if="selectedRadio==='removeGoods'"
                     :arrayGoods="arrayGoods"
                     :arrayGroup="arrayGroup"
                     @remove-goods="$emit('remove-goods',$event)"></RemoveGoods>
    </section>
</template>

<script>
import NewGoods from "@/components/NewGoods.vue";
import NewGroup from "@/components/NewGroup.vue";
import RemoveGoods from "@/components/RemoveGoods.vue";
import RemoveGroup from "@/components/RemoveGroup.vue";
import SelectionOfAction from "@/components/SelectionOfAction.vue";

export default {
    name: "Admin",
    props: ['arrayGroup', 'arrayGoods', 'pickedGoods'],
    emits: ['add-new-group', 'add-new-good', 'remove-group', 'remove-goods'],
    components: {
        RemoveGoods,
        RemoveGroup,
        NewGoods,
        NewGroup,
        SelectionOfAction
    },
    data() {
        return {
            selectedRadio: ''
        };
    }
};
</script>

<style scoped>
#admin {
    background-color: #76b35d;
}

#admin::after {
    content: '';
    display: table;
    clear: both;
}
</style>
