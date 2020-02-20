<template>
    <div id="app">
        <div id="label-bar">
            <h4>Your boxes</h4>
            <ul>
                <li v-for="(box, i) in boxes" :key="i"
                    v-bind:class="{'active': i===activeBoxIndex}">
                    <input v-model="box.label"
                           v-on:click="makeBoxActive(i)"/>
                    <a @click="removeBox(i)">x</a>
                </li>
            </ul>
        </div>
        <div id="image-wrapper" :style="{backgroundImage: `url(caterpillar.jpg)`}"
             @mousedown="startDrawingBox"
             @mousemove="changeBox"
             @mouseup="stopDrawingBox">
            <Box v-if="drawingBox.active"
                 :b-width="drawingBox.width"
                 :b-height="drawingBox.height"
                 :b-top="drawingBox.top"
                 :b-left="drawingBox.left"/>
            <Box v-for="(box, i) in boxes" :key="i"
                 :b-top="box.top" :b-left="box.left"
                 :b-label="box.label"
                 :b-width="box.width" :b-height="box.height"
                 :b-active="i===activeBoxIndex"
                 :on-select="makeBoxActive" :b-index="i"
                 :on-delete="removeBox"
            />
        </div>
    </div>
</template>

<script>
    import Box from "./components/Box";
    import {pick} from 'lodash';

    const getCoursorLeft = (e) => {
        return e.pageX - 10;
    };

    const getCoursorTop = (e) => {
        return e.pageY - 10;
    };

    export default {
        name: 'app',
        components: {Box},
        data: function () {
            return {
                drawingBox: {
                    active: false,
                    top: 0,
                    left: 0,
                    height: 0,
                    width: 0
                },
                boxes: [],
                activeBoxIndex: null,
            }
        },
        methods: {
            startDrawingBox(e) {
                this.drawingBox = {
                    width: 0,
                    height: 0,
                    top: getCoursorTop(e),
                    left: getCoursorLeft(e),
                    active: true,
                };
            },
            changeBox(e) {
                if (this.drawingBox.active) {
                    this.drawingBox = {
                        ...this.drawingBox,
                        width: getCoursorLeft(e) - this.drawingBox.left,
                        height: getCoursorTop(e) - this.drawingBox.top,
                    };
                }
            },
            stopDrawingBox() {
                if (this.drawingBox.active) {
                    if (this.drawingBox.width > 5) {
                        this.boxes.push({...pick(this.drawingBox, ['width', 'height', 'top', 'left'])});
                    }
                    this.drawingBox = {
                        active: false,
                        top: 0,
                        left: 0,
                        height: 0,
                        width: 0
                    }
                }
            },
            makeBoxActive(i) {
                this.activeBoxIndex = i;
            },
            removeBox(i) {
                this.boxes = this.boxes.filter((elem, index) => {
                    return index !== i;
                });
                this.activeBoxIndex = null;
            },
        }
    }
</script>

<style lang="scss" scoped>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;

        #image-wrapper {
            height: 640px;
            width: 640px;
            background-repeat: no-repeat;
            position: relative;
        }

        #label-bar {
            float: right;
            margin-right: 50px;
            width: 220px;

            ul {
                padding: 0;

                li {
                    list-style-type: none;
                    padding: 8px 16px;

                    &.active {
                        background-color: lightblue;
                    }

                    a {
                        cursor: pointer;
                        display: inline-block;
                        margin-left: 4px;
                        font-weight: bold;
                        color: red;
                    }
                }
            }
        }
    }

</style>
