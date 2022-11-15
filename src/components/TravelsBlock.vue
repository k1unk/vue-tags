<template>
    <div class="travels-block">
        <Travel v-for="travel in travels" :travel="travel" :travelSelected="travelSelected" @changeSelected="changeSelected"/>
    </div>
</template>

<script>
import Travel from "@/components/Travel";

export default {
    name: 'TravelsBlock',
    props: {
        travels: Array,
        travelSelected: Number
    },
    components: {
        Travel
    },
    methods:{
        changeSelected(id) {
            this.$emit('changeSelected', id)
        }
    }
}
</script>
