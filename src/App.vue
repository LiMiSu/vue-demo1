<template>
    <div class="wrapper">
        <div>第{{n}}手</div>
        <div class="row">
            <!--<Cell @click="(0)=>onClickCell(0)" :n="n"/>  实际上正确写法应该是这样，但是vue做了一个语法糖，
            如果发现你直接调用了一个函数，这个函数不会直接调用，它就会等click的时候再去调用这个函数。
             而不是我们看到的一个函数后面加个括号（）就会马上调用函数的意思
             就是如果你在click里面写函数执行的代码，它就猜你是想在点击的时候执行-->
            <Cell @click="onClickCell(0, $event)" :n="n"/>
            <Cell @click="onClickCell(1, $event)" :n="n"/>
            <Cell @click="onClickCell(2, $event)" :n="n"/>
        </div>
        <div class="row">
            <Cell @click="onClickCell(3, $event)" :n="n"/>
            <Cell @click="onClickCell(4, $event)" :n="n"/>
            <Cell @click="onClickCell(5, $event)" :n="n"/>
        </div>
        <div class="row">
            <Cell @click="onClickCell(6, $event)" :n="n"/>
            <Cell @click="onClickCell(7, $event)" :n="n"/>
            <Cell @click="onClickCell(8, $event)" :n="n"/>
        </div>
        <div>
            结果：{{result===null?'胜负未分':`胜方为${result}`}}
        </div>
    </div>
</template>
<script>
    import Cell from "./Cell";

    export default {
        components: {Cell},
        data() {
            return {
                n: 0,
                map: [
                    [null, null, null],
                    [null, null, null],
                    [null, null, null]
                ],
                result: null
            }
        },
        methods: {
            onClickCell(i, text) {
                console.log(`${i}号被点击，内容是：${text}}`);
                this.map[Math.floor(i / 3)][i % 3] = text;
                this.n += 1;
                this.tell();
            },
            tell() {
                const map = this.map;

                //横
                for (let i = 0; i < 2; i++) {
                    if (map[i][0] !== null &&
                        map[i][0] === map[i][1] &&
                        map[i][1] === map[i][2]
                    ) {
                        this.result = map[i][0];
                    }
                }
                //纵
                for (let j = 0; j < 2; j++) {
                    if (map[0][j] !== null &&
                        map[0][j] === map[1][j] &&
                        map[1][j] === map[2][j]
                    ) {
                        this.result = map[0][j];
                    }
                }
                //斜
                if (map[0][0] !== null &&
                    map[0][0] === map[1][1] &&
                    map[1][1] === map[2][2]
                ) {
                    this.result = map[0][0];
                }
                if (map[0][2] !== null &&
                    map[0][2] === map[1][1] &&
                    map[1][1] === map[2][0]
                ) {
                    this.result = map[0][2];
                }
            }
        }
    }
</script>

<style>
    .row {
        display: flex;
    }
    .wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction:column;
    }
</style>
