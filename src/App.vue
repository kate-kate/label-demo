<template>
    <div id="app">
        <h1>Object Labelling Demo</h1>
        <div id="image-wrapper" :style="{backgroundImage: `url(caterpillar.jpg)`}">
          <Box b-top="135" b-left="200" b-width="190" b-height="390"/>
        </div>
    </div>
</template>

<script>

    import Box from "./components/Box";
    export default {
        name: 'app',
        components: {Box},
    }
</script>

<style lang="scss" scoped>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;

        #image-wrapper {
            height: 640px;
            width: 640px;
            background-repeat: no-repeat;
            position: relative;
        }
    }

</style>
