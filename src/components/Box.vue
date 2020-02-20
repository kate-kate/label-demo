<template>
    <div class="box-wrapper">
        <div class="label"
             v-if="bLabel"
             :style="{
                 top: (bTop - 10) + 'px',
                 left: bLeft + 'px',
                 width: (bWidth + 4) + 'px'}">
            {{ bLabel }}
        </div>
        <a class="box-delete"
           v-on:click="removeMyself"
           v-if="bActive"
           :style="{
               top: (bTop - 18) +'px',
               left: (bLeft + bWidth) + 'px'
               }">
            x
        </a>
        <div class="box" :style="{
                 top: bTop + 'px',
                 left: bLeft + 'px',
                 width: bWidth + 'px',
                 height: bHeight + 'px'
             }"
             v-bind:class="{'active': bActive}"
             @mousedown="selectBox"
        >
        </div>
    </div>
</template>

<script>
    export default {
        name: "Box",
        props: [
            'b-top', 'b-left', 'b-width', 'b-height', 'b-label',
            'on-select', 'b-active', 'b-index', 'on-delete'
        ],
        methods: {
            selectBox() {
                this.onSelect(this.bIndex)
            },
            removeMyself() {
                this.onDelete(this.bIndex)
            },
        }
    }
</script>

<style lang="scss" scoped>
    .box {
        position: absolute;
        border: 2px #90ee90 solid;

        &:hover, &.active {
            background-color: rgba(144, 238, 144, .2);
        }

        z-index: 3;
    }
    .label {
        position: absolute;
        height: 22px;
        font-size: 16px;
        color: #000;
        font-weight: bold;
        background-color: #90ee90;
        z-index: 4;
    }
    .box-delete {
        position: absolute;
        z-index: 6;
        font-weight: bold;
        color: red;
        cursor: pointer;
        font-size: 24px;
        font-weight: bold;
    }
</style>