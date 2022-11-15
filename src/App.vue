<template>
    <v-app>
        <Container/>
    </v-app>
</template>

<script>
import Container from './components/Container';

export default {
    name: 'App',
    components: {
        Container
    },

};
</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>
