<template>
    <div :class="getClass()" @click="changeSelected">
        <TravelTitle :title="travel.title"/>
        <TravelTags :tags="travel" :isSelected="isSelected()" :alignCenter="getAlign()"/>
    </div>
</template>

<script>
import TravelTitle from "@/components/TravelTitle";
import TravelTags from "@/components/TravelTags";

export default {
    name: 'Travel',
    components: {TravelTitle, TravelTags},

    props: {
        travel: Object,
        travelSelected: Number
    },
    methods: {
        getAlign() {
            return Math.random() < 0.5
        },
        isSelected() {
            return this.travelSelected === this.travel.id
        },
        getClass() {
            if (this.travelSelected === this.travel.id) return "travel travel_selected"
            else return "travel"
        },
        changeSelected() {
            this.$emit('changeSelected', this.travel.id)
        }
    }
}
</script>

<style lang="scss" scoped>
.travel {
    margin: 10px;
    padding: 0 5px;
    border-bottom: 1px solid grey;

    &:hover {
        cursor: pointer;
        background-color: antiquewhite;
    }
}

.travel_selected {
    color: #ffcd6a;
}

</style>
