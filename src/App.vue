<template>
    <section id="mainApp">
        <User :arrayGoods="arrayGoods"
              :arrayGroup="arrayGroup"
              :errorMessage="errorMessage"
              :pickedGoods="pickedGoods"
              @delete-picked-good="deletePickedGood"
              @error-message="errorMessage=$event"
              @add-to-picked-goods="addToPickedGoods"></User>
        <Admin :arrayGoods="arrayGoods"
               :arrayGroup="arrayGroup"
               :pickedGoods="pickedGoods"
               @add-new-group="addNewGroup"
               @add-new-good="addNewGood"
               @remove-group="removeGroup"
               @remove-goods="removeGoods"></Admin>
    </section>
</template>

<script>

import Admin from "@/components/Admin.vue";
import User from "@/components/User.vue";

export default {
    name: 'App',
    components: {
        Admin,
        User
    },
    emits: [],
    data() {
        return {
            pickedGoods: [],
            errorMessage: '',
            arrayGroup: [{
                value: 'fruits',
                name: 'fresh fruits'
            }, {
                value: 'drinks',
                name: 'drinks'
            }, {
                value: 'coffee',
                name: 'coffee'
            }, {
                value: 'appliances',
                name: 'home appliances'
            }],
            arrayGoods: [{
                group: 'fruits',
                value: 'avocado',
                name: 'avocado'
            }, {
                group: 'fruits',
                value: 'banana',
                name: 'banana'
            }, {
                group: 'fruits',
                value: 'blackberries',
                name: 'blackberries'
            }, {
                group: 'fruits',
                value: 'mango',
                name: 'mango'
            }, {
                group: 'fruits',
                value: 'grožđe',
                name: 'grožđe'
            }, {
                group: 'fruits',
                value: 'kumkvata',
                name: 'kumkvata'
            }, {
                group: 'fruits',
                value: 'breskva',
                name: 'breskva'
            }, {
                group: 'drinks',
                value: 'rakija',
                name: 'rakija'
            }, {
                group: 'drinks',
                value: 'orange',
                name: 'orange soda'
            }, {
                group: 'drinks',
                value: 'milk',
                name: 'fresh milk'
            }, {
                group: 'drinks',
                value: 'paulaner',
                name: 'paulaner'
            }, {
                group: 'drinks',
                value: 'valjevsko',
                name: 'valjevsko'
            }, {
                group: 'drinks',
                value: 'tuborg',
                name: 'tuborg'
            }, {
                group: 'coffee',
                value: 'turkish',
                name: 'turkish coffee'
            }, {
                group: 'coffee',
                value: 'cappuccino',
                name: 'cappuccino'
            }, {
                group: 'coffee',
                value: 'latte',
                name: 'latte'
            }, {
                group: 'coffee',
                value: 'grand',
                name: 'grand'
            }, {
                group: 'coffee',
                value: 'cappuccino',
                name: 'cappuccino'
            }, {
                group: 'coffee',
                value: 'espresso',
                name: 'espresso'
            }, {
                group: 'coffee',
                value: 'vacuum',
                name: 'vacuum coffee'
            }, {
                group: 'appliances',
                value: 'dishwasher',
                name: 'dishwasher'
            }, {
                group: 'appliances',
                value: 'microwaves',
                name: 'microwaves'
            }, {
                group: 'appliances',
                value: 'ranges',
                name: 'ranges'
            }]
        };
    },
    methods: {
        addToPickedGoods(newValue) {
            this.pickedGoods.push(newValue);
        },
        deletePickedGood(good) {
            this.pickedGoods = this.pickedGoods.filter((el) => el !== good);
        },
        addNewGroup(newGroupToAdd) {
            this.arrayGroup.push({
                value: newGroupToAdd,
                name: newGroupToAdd
            });
        },
        addNewGood(newGoodToAdd) {
            this.arrayGoods.push(newGoodToAdd);
        },
        removeGroup(groupToRemove) {
            this.arrayGroup = this.arrayGroup.filter(el => el.value !== groupToRemove);
        },
        removeGoods(goodToRemove) {
            this.arrayGoods = this.arrayGoods.filter(el => el.value !== goodToRemove);
            this.pickedGoods = this.pickedGoods.filter(el => el !== goodToRemove);
        }
    }
};
</script>

<style>
* {
    box-sizing: border-box;
}

body, html, #app {
    margin: 0;
    padding: 0;
    height: 100%
}

#app {
    max-width: 700px;
    margin: 0 auto 0;
    overflow: auto;
    background-color: #76b35d;
}

#mainApp {
    margin: 0;
    padding: 0;
}

p {
    margin: 0;
}
</style>
