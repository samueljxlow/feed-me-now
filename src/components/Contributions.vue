<template>
    <div id="mainContainer">
        <PageHeader v-bind:header="'Your Contributions'" v-bind:icon="'heart'"/>
        <div class="row">
            <div class="column" v-for="([animalId, array], index) in Object.entries(contributionList)" :key="index">
                <ContributionCard v-bind:animalId="animalId" v-bind:array="array"/>
            </div>
        </div>
    </div>
</template>
<script>
import PageHeader from "./PageHeader.vue"
import ContributionCard from './ContributionCard.vue';
import database from "../firebase.js";

export default {
    name: "Contributions",
    components: {
        ContributionCard,
        PageHeader
    },
    data() {
        return {
            // animalList: [],
            currUser: "QNqhGFZ0EVtmArEaV3vt",
            contributionList: null,
        }
    },
    methods: {
        fetchContributions: function() {
            database.collection('users').doc(this.currUser).get().then(doc => {
                this.contributionList = doc.data().contributions
            }).then(() =>{
                console.log(this.contributionList)
            })
        }
    },
    created() {
        this.fetchContributions();
    }
}
</script>
<style scoped>
#mainContainer {
    align-items: center;
}
.row {
    display: flex;
    flex-wrap: wrap;
}
.row>* {
    flex: 0 0 33.3333%;
    min-width: 410px;
    max-width: none;
    max-height: 550px;
}
.row:after {
    display: table;
    clear: both;
}
.column {
    float:left;
}
</style>