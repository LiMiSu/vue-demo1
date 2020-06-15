<template>
    <div>
        <div class="cell" @click="onClickSelf">
            <template v-if="a">{{text}}</template>
            <template v-else></template>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["n"],
        data() {
            return {a: false, text: ''}
        },
        methods: {
            onClickSelf() {
                if (this.text !== ''){
                    return;
                }
                this.a = true;
                this.text = this.n % 2 === 0 ? "X" : "O";
                this.$emit('click', this.text)
            }
        }
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box
    }

    .cell {
        border: 1px solid black;
        width: 100px;
        height: 100px;
        /*让字居中 当然也可以用其他*/
        display: flex;
        justify-content: center;
        align-items: center;
        /*其他1*/
        /*text-align: center;*/
        /*line-height: 100px;*/
        font-size: 80px;
    }
</style>
