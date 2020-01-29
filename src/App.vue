<template>
    <div id="app">
        <h1>Object Labelling Demo</h1>
        <div id="image-wrapper" :style="{backgroundImage: `url(caterpillar.jpg)`}">
          <div class="box" :style="{top: '135px', left: '200px', width: '190px', height: '390px'}">
          </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'app',
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

            .box {
                position: absolute;
                border: 2px #90ee90 solid;
                &:hover, &.active {
                    background-color: rgba(144, 238, 144, .2);
                }
                z-index: 3;
            }
        }
    }

</style>
