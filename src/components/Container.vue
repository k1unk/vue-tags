<template>
    <div class="travels-container">
        <div class="block travels-wrapper" ref="travelsWrapper">
            <TravelsBlock :travels="travels" :travelSelected="travelSelected" @changeSelected="changeSelected"/>
        </div>
        <div class="slider" @mousedown="drag"></div>
        <div class="block chosen-travel">
            <p v-if="!travelSelected">Travels not selected</p>
            <p v-else>{{ getTitle() }}</p>
        </div>
    </div>
</template>

<script>
import TravelsBlock from "@/components/TravelsBlock";

export default {
    name: 'Container',
    props: {
        msg: String
    },
    components: {
        TravelsBlock,
    },
    data() {
        return {
            travelSelected: 2,
            travels: [
                {
                    id: 1,
                    title: "Город сыра и мира",
                    stars: 5,
                    type: "historical",
                    transport: "bus",
                    date: "28 Марта",
                    time: 9,
                    peopleMax: 1111,
                    displayPosition: "left"
                },
                {
                    id: 2,
                    title: "Экскурсия в национальный парк Куршская коса",
                    stars: 5,
                    type: "sightseeing",
                    transport: "bus",
                    date: "25 Марта",
                    time: 6,
                    peopleMax: 1314,
                    displayPosition: "left"
                },
                {
                    id: 3,
                    title: "О кирках, рыцарях и замках",
                    stars: 5,
                    type: "historical",
                    transport: "bus",
                    date: "29 Марта",
                    time: 6,
                    peopleMax: 1,
                    displayPosition: "center"
                },
                {
                    id: 4,
                    title: "О кирках, рыцарях и замках",
                    stars: 5,
                    type: "historical",
                    transport: "bus",
                    date: "29 Марта",
                    time: 6,
                    peopleMax: 1,
                    displayPosition: "left"
                },
                {
                    id: 5,
                    title: "Экскурсия в янтарный",
                    stars: null,
                    type: "historical",
                    transport: "bus",
                    date: "29 Марта",
                    time: 6,
                    peopleMax: 49,
                    displayPosition: "left"
                },
            ]
        }
    },
    methods: {
        drag: function (e) {
            let dragX = e.clientX;
            let block = this.$refs.travelsWrapper;
            document.onmousemove = function onMouseMove(e) {
                block.style.width = block.offsetWidth + e.clientX - dragX + "px";
                dragX = e.clientX;
            }
            document.onmouseup = () => document.onmousemove = document.onmouseup = null;
        },
        getTitle() {
            for (const travel of this.travels) {
                if (travel.id === this.travelSelected) return "id: " + travel.id + ", title: " + travel.title
            }
        },
        changeSelected(id) {
            this.travelSelected = id
        }
    }

}
</script>

<style lang="scss" scoped>
.travels-container {
    width: 1200px;
    margin: 50px auto 0 auto;
    display: flex;
    justify-content: center;
    background-color: #ffffff;

    .block {
        width: 50%;
        min-width: 300px;
        border: 1px solid black;
    }

    .chosen-travel {
        flex: 1;

        p {
            text-align: center;
        }
    }

    .slider {
        width: 7px;
        cursor: col-resize;
        user-select: none;
        background-color: #262626;
    }
}

</style>
