<template>
    <div class="travel__title">
       {{ title }}
    </div>
</template>

<script>
export default {
    name: 'TravelTitle',
    props: {
        title: String
    },
}
</script>

<style lang="scss" scoped>
.travel__title {
    font-size: 16px;
}

</style>
