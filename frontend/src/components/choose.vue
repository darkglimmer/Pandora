<template>
    <div class="parent">
        <div class="mask" v-if = "flag"></div>

        <div id="new" class="choice" @click="add('neww')"></div>
        <div id="study" class="choice" @click="add('study')"></div>
        <div id="food" class="choice" @click ="add('food')"></div>
        <div id="know" class="choice" @click="add('know')"></div>
        <div id="health" class="choice" @click="add('health')"></div>
        <div id="friend" class="choice" @click="add('friend')"></div>
        <div id="weigh" class="choice" @click="add('weigh')"></div>
        <div id="travel" class="choice" @click="add('travel')"></div>
        <button class="but" @click="check">确定</button>

        <div class="dialog" v-if="flag" >
            <div class="title"  >点击单元格可修改具体内容</div>
            <div class="content">
                <v-table
                    is-horizontal-resize
                    style="width:100%"
                    :columns="columns"
                    :table-data="tableData"
                    row-hover-color="#eee"
                    row-click-color="#edf7ff"
                    :cell-edit-done="cellEditDone"
                ></v-table>

                <div>
                    <div class="submit " @click = "checked()" >保存</div>
                </div>
            </div>
        </div> 
    </div>
</template>

<script>
export default {
    name: 'choose',
    data () {
        return{
            choosed:[],
            flag: false,
            task: {
                "neww": {"task":"了解周边","time":"1.5h","ddl":"7.25"},
                "study": {"task":"阅读书籍","time":"1wk","ddl":"7.30"},
                "food": {"task":"品尝一道美食","time":"2h","ddl":"7.26"},
                "health": {"task":"早睡早起","time":"1wk","ddl":"7.30"},
                "friend": {"task1":"和旧友聊天","time":"1h","ddl":"7.25"},
                "know": {"task":"去探索新世界！","time":"","ddl":"8.1"},
                "travel": {"task":"去上海玩吧","time":"3d","ddl":"8.1"},
                "weigh": {"task":"不吃油炸食品","time":"1wk","ddl":"8.1"}

            },
            tableData: [
                    // {"task":"学习","time":"","ddl":"7.25",},
                    // {"task":"运动","time":"","ddl":"7.26",},
                    // {"task":"旅游","time":"","ddl":"7.26",},
                    // {"task":"减肥","time":"","ddl":"7.26",},
                    // {"task":"品尝美食","time":"","ddl":"7.26",}
                ],
            columns: [
                    {field: 'task', title:'任务', width: 120, titleAlign: 'center',columnAlign:'center',isEdit:true,
                              formatter: function (rowData,rowIndex,pagingIndex,field) {
                                   return `<span class='cell-edit-color'>${rowData[field]}</span>`;
                               }},
                    {field: 'time', title: '持续时间', width: 90, titleAlign: 'center',columnAlign:'center',isEdit:true,},
                    {field: 'ddl', title: '截止时间', width: 90, titleAlign: 'center',columnAlign:'center',isEdit:true,},
            ]
        }
    },
    mounted(){
    },
    methods: {
        add(str){
            if(this.choosed.indexOf(str)<0){
                this.choosed.push(str);
                this.tableData.push(this.task[str]);
            }
            // console.log(this.choosed);
        },
        check(){
            this.flag = !this.flag;
            
        },
        checked(){
            this.flag = !this.flag;
            // fetch()
            this.$router.push("/main");
        },
        cellEditDone(newValue,oldValue,rowIndex,rowData,field){
            this.tableData[rowIndex][field] = newValue;
        }

    }
}
</script>

<style>
.parent{
    background-image: url(http://p9lce13x8.bkt.clouddn.com/choice.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    width: 100%;
    height: 100%;
    min-height: 667px;
    display: block;
    position: absolute;
    top:0;
    left:0;
    text-align: center;
}

.cell-edit-color{
    color:#2db7f5;
    font-weight: bold;
}

.choice{
    /* background:black; */
    position: absolute;
    /* opacity:0.4; 
    filter: Alpha(opacity=40); */
}
.but{
    width: 120px;
    height: 40px;
    background: #b9c0ff;
    font-size: 18px;
    color: #666666;
    border-width: 0;
	border-radius: 5px; 
    outline: none;
    margin-top: 550px;
    vertical-align: middle;
    
}
.but:hover{
    background:  #aab2ff;
    color: black;
}
#new{
    width:50px;
    height:50px;
    border-radius: 25px;
    top:20%;
    left:25%;
}
#study{
    width:70px;
    height:60px;
    border-radius: 30px;
    top:23%;
    left:45%;

}
#food{
    width:100px;
    height:60px;
    border-radius: 50px;
    top:30%;
    left:60%;
    transform:rotate(-15deg);
}
#know{
    width:60px;
    height:30px;
    border-radius: 15px;
    top:20%;
    left:76%; 
    transform:rotate(-15deg);
}
#health{
    width:100px;
    height:60px;
    border-radius: 50px;
    top:29%;
    left:10%;
    transform:rotate(15deg);
}
#friend{
    width:80px;
    height:60px;
    border-radius: 50px;
    top:40%;
    left:20%;
    transform:rotate(15deg);
}
#travel{
    width:80px;
    height:60px;
    border-radius: 50px;
    top:52%;
    left:3%;
    transform:rotate(15deg);
}
#weigh{
    width:80px;
    height:60px;
    border-radius: 50px;
    top:41%;
    left:73%;
    transform:rotate(15deg);

}
.dialog{
    width: 340px;
    height: 90%;
    min-height: 450px;
    /* display: none; */
    position: absolute;
    top: 30px;
    left: 17px;
    z-index: 9000;
    border: 1px solid #D5D5D5;
    background: #fff;
}
.title{
    height: 48px;
    line-height: 48px; 
    padding:0px 20px;
    color: #535353;
    font-size: 16px;
    border-bottom: 1px solid #efefef;
    background: #f5f5f5; 
}
.content{
    padding: 15px 20px;
    height:100px;
}

.submit{
    width: 300px;
    height: 50px;
    background: #3b7ae3;
    border:none;
    font-size: 16px;
    color: #fff;
    outline: none;
    text-decoration: none;
    display: block;
    text-align: center;
    line-height: 50px;
    position: absolute;
    bottom: 15px;
}
.submit:hover{
    background: #3f81b0;
}
.mask{
    width: 100%;
    height:100%;
    background: #000;
    position: absolute;
    top: 0px;
    z-index: 8000;
    opacity:0.4; 
    filter: Alpha(opacity=40);
}


</style>
