<template>
    <div class="contianer">
        <div class="msg">
            {{msg}}
        </div>
        <div class="main">
            <!--棋盘-->
            <div class="square">
                <!-- <div v-for="(item,i) in chessResult" v-bind:key="i">
                    <div class="cell" @click="move(i)">
                        <div>{{ item }}</div>
                    </div>
                </div> -->
                <div class="row">
                    <div class="cell" @click="move(0)">
                        <div>{{ chessResult[0] }}</div>
                    </div>
                    <div class="cell" @click="move(1)">
                        <div>{{ chessResult[1] }}</div>
                    </div>
                    <div class="cell" @click="move(2)">
                        <div>{{ chessResult[2] }}</div>
                    </div>
                </div>
                <div class="row">
                    <div class="cell" @click="move(3)">
                        <div>{{ chessResult[3] }}</div>
                    </div>
                    <div class="cell" @click="move(4)">
                        <div>{{ chessResult[4] }}</div>
                    </div>
                    <div class="cell" @click="move(5)">
                        <div>{{ chessResult[5] }}</div>
                    </div>
                </div>
                <div class="row bottom">
                    <div class="cell" @click="move(6)">
                        <div>{{ chessResult[6] }}</div>
                    </div>
                    <div class="cell" @click="move(7)">
                        <div>{{ chessResult[7] }}</div>
                    </div>
                    <div class="cell" @click="move(8)">
                        <div>{{ chessResult[8] }}</div>
                    </div>
                </div>
            </div>
            <!--记录-->
            <!-- <div class="log">

            </div> -->
        </div>
    </div>
</template>

<script>

export default {
    name: 'HelloWorld',
    data(){
        return{
            //落子结果
            chessResult: [
                '', '', '',
                '', '', '',
                '', '', ''
            ],
            winResult: [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6]
            ],
            
            msg: 'welcome',
            whoIsNext: 'X',
            matchEnd: false,


            test: ''
        }
    },
    methods: {
        move(id){
            const _this = this
            if(_this.matchEnd){
                return
            }
            
            let changeResult = _this.chessResult
            changeResult[id] = (function(){
                if(_this.whoIsNext === 'X'){
                    _this.whoIsNext = 'O'
                    return 'X'
                }else{
                    _this.whoIsNext = 'X'
                    return 'O'
                }
            })()
            _this.chessResult = changeResult

            _this.resultCheck()
        },
        resultCheck(){
            let _this = this
            let chessResult = this.chessResult
            let winResult = this.winResult
            for(let i in winResult){
                let arr = winResult[i]
                if(chessResult[arr[0]] === chessResult[arr[1]] 
                  && chessResult[arr[0]] === chessResult[arr[2]]
                  && chessResult[arr[1]] === chessResult[arr[2]]
                  && chessResult[arr[0]] !== ''
                  && chessResult[arr[1]] !== ''
                  && chessResult[arr[2]] !== ''){
                    // console.log(1)
                   _this.matchEnd = true
                   _this.msg = 'winner is ' + chessResult[arr[0]]
                   return
                }
            }
            _this.msg = 'next is ' + _this.whoIsNext
        }

    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .msg{
        margin-bottom: 20px;
    }
    .main{
        display: flex;
        justify-content: center;
    }
    .row{
        display: flex;
        border-left: 1px solid;
        width: 150px;
    }
    .cell{
        width: 50px;
        height: 50px;
        border-right: 1px solid;
        border-top: 1px solid;

        display: flex;
        justify-content: center;
        align-items: center;
    }
    .bottom .cell{
        border-bottom: 1px solid;
    }
    
</style>
