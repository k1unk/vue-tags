<template>
    <div :class="tagsClass()" ref="tags" @click="hideElements" :style="isAlignCenter()">
        <div class="tag" ref="tagStars" v-if="tags.stars">
            <v-icon small :color="getColor()" class="mr-1"> mdi-star-outline</v-icon>
            <div>{{ tags.stars }}</div>
        </div>
        <div class="tag" ref="tagType" v-if="tags.type">
            <div>{{ tags.type === 'historical' ? 'Историческая' : 'Обзорная' }}</div>
        </div>
        <div class="tag" ref="tagTransport" v-if="tags.transport">
            <v-icon small :color="getColor()" class="mr-1"> mdi-bus</v-icon>
            <div>{{ tags.transport === 'bus' ? 'На автобусе' : 'На поезде' }}</div>
        </div>
        <div class="tag" ref="tagDate" v-if="tags.date">
            <div>{{ tags.date }}</div>
        </div>
        <div class="tag" ref="tagTime" v-if="tags.time">
            <v-icon small :color="getColor()" class="mr-1"> mdi-clock-time-three-outline</v-icon>
            <div>{{ tags.time }}</div>
        </div>
        <div class="tag" ref="tagPeopleMax" v-if="tags.peopleMax">
            <v-icon small :color="getColor()" class="mr-1"> mdi-account</v-icon>
            <div>до {{ tags.peopleMax }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Travel',
    props: {
        tags: Object,
        alignCenter: Boolean,
        isSelected: Boolean
    },
    data() {
        return {
            tagsToShow: [],
            resizeObserver: null,
            refs: []
        }
    },
    methods: {
        isAlignCenter(){
             return this.alignCenter ? 'justify-content: space-between' : 'justify-content: left'
        },
        getColor() {
            return this.isSelected ? '#ffcd6a' : '#949494'
        },
        tagsClass() {
            return this.isSelected ? 'tags tags_selected' : 'tags'
        },
        createTagsArray() {
            if (this.tags.stars) {
                this.tagsToShow.push({stars: this.tags.stars})
                this.refs.push(this.$refs.tagStars)
            }
            if (this.tags.type) {
                this.tagsToShow.push({type: this.tags.type})
                this.refs.push(this.$refs.tagType)
            }
            if (this.tags.transport) {
                this.tagsToShow.push({transport: this.tags.transport})
                this.refs.push(this.$refs.tagTransport)
            }
            if (this.tags.date) {
                this.tagsToShow.push({date: this.tags.date})
                this.refs.push(this.$refs.tagDate)
            }
            if (this.tags.time) {
                this.tagsToShow.push({time: this.tags.time})
                this.refs.push(this.$refs.tagTime)
            }
            if (this.tags.peopleMax) {
                this.tagsToShow.push({peopleMax: this.tags.peopleMax})
                this.refs.push(this.$refs.tagPeopleMax)
            }
        },
        hideElements() {
            let overflow = false
            this.refs.forEach((el) => {
                if (overflow) {
                    el.style.display = 'none'
                } else {
                    if (el.style.display === 'none') el.style.display = 'flex'
                    if (el.previousElementSibling) {
                        if (el.offsetLeft < el.previousElementSibling.offsetLeft) {
                            el.style.display = 'none'
                            overflow = true
                            console.log(14);
                        } else {
                            el.style.display = 'flex'
                            overflow = false
                        }
                    }
                }
            });
        },
    },
    mounted() {
        this.createTagsArray()
        this.resizeObserver = new ResizeObserver(this.hideElements)
        this.resizeObserver.observe(this.$refs.tags)
        this.hideElements()
    },
    beforeDestroy() {
        this.resizeObserver.unobserve(this.$refs.tags)
    }

}
</script>

<style lang="scss" scoped>
.tags {
    display: flex;
    flex-wrap: wrap;
    color: #949494;

    .tag {
        margin-left: 15px;
        position: relative;
        display: flex;
        align-items: baseline;

        &::before {
            content: "\A";
            width: 4px;
            height: 4px;
            top: 5px;
            left: 0;
            transform: translate(0, -3px);
            margin-right: 15px;
            border-radius: 50%;
            background: #3a3a3a;
            display: inline-block;
        }

        &:first-child {
            margin-left: 0;

            &:before {
                display: none;
            }
        }
    }
}

.tags_selected {
    color: #ffcd6a;

    .tag:before {
        background: #ffcd6a;
    }
}
</style>
