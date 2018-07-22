<template>
  <div>
    <img src="http://p9lce13x8.bkt.clouddn.com/black.png" v-if="success" class="black">
    <div v-if="success">
      <img src="http://p9lce13x8.bkt.clouddn.com/quit_choice.png" class="quit_choice">
      <div class="choicequit" @click="choice_quit">退出</div>
      <div class="cancel" @click="cancel">取消</div>
    </div>
    <div v-if="show" class="white">
      <div class="new_title">新个人任务</div>
      <div class="new_rask">任务优先级：
        <input type="text" class="input">
      </div>
      <div class="new_rask">任务名称：
        <input type="text" class="input">
      </div>
      <div class="new_rask">所需名称：
        <input type="text" class="input">
      </div>
      <div class="new_rask">截止日期：
        <input type="text" class="input">
      </div>
      <button class="button" @click="yes">是</button>
      <button class="button" @click="no">否</button>
    </div>
    <div v-if="movie" class="white">
      <div class="new_title">修改任务</div>
      <div class="new_rask">任务优先级：
        <input type="text" class="input">
      </div>
      <div class="new_rask">任务名称：
        <input type="text" class="input">
      </div>
      <div class="new_rask">所需名称：
        <input type="text" class="input">
      </div>
      <div class="new_rask">截止日期：
        <input type="text" class="input">
      </div>
      <button class="button" @click="change_yes">是</button>
      <button class="button" @click="change_no">否</button>
    </div>
    <div v-if="check" class="check_money">
      <div class="tip">提示</div>
      <div class="contact">确认要花费$20来修改任务</div>
      <button class="button_1" @click="Y">是</button>
      <button class="button_1" @click="N">否</button>
    </div>
    <div class="main">
      <div class="top">
        <img src="http://p9lce13x8.bkt.clouddn.com/%3C.png" class="arrow" @click="back">
      </div>
      <div class="head">
        <div class="square">
          <img src="http://oqz8dkpuh.bkt.clouddn.com/fat_girl.png" v-if="!good" class="girl">
          <img src="http://oqz8dkpuh.bkt.clouddn.com/girl.png" v-if="good" class="girl">
        </div>
        <div class="self">
          <div class="id_1">ID: {{username}}</div>
          <div class="id_2">
            <img src="http://p9lce13x8.bkt.clouddn.com/money.png" class="dollar">
            {{score}}
          </div>
          <div>
            <div class="aim">固定目标</div>
            <el-progress class="progress" :text-inside="true" :stroke-width="18" :percentage="sstaus" color="#ffaaae"></el-progress>
            <div class="aim">个人目标</div>
            <el-progress class="progress" :text-inside="true" :stroke-width="18" :percentage="pstatus" color="#ed7d99"></el-progress>
          </div>
          <div class="time" prop="time">当前时间：</div>
        </div>
      </div>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column fixed prop="importance" label="优先级" width="80">
        </el-table-column>
        <el-table-column prop="name" label="任务" width="300">
        </el-table-column>
        <el-table-column prop="hour" label="所需时间(h/天)" width="80">
        </el-table-column>
        <el-table-column prop="ddl" label="截止时间" width="80">
        </el-table-column>
        <el-table-column label="操作" width="100">
          <template slot-scope="scope">
                  <el-button @click="deleteRow(scope.$index, scope.row)" type="text" size="small">删除</el-button>
                  <el-button @click="changeRow(scope.$index, scope.row)" type="text" size="small">编辑</el-button>
</template>
      </el-table-column>
      <el-table-column
      fixed="right"
      prop="result"
      label="完成情况"
      width="80">
<template slot-scope="scope">
  <el-button size="mini" v-if="!done" @click="finish(scope.$index, scope.row)">
    已完成</el-button>
  <img src="http://p9lce13x8.bkt.clouddn.com/correct.png" v-if="done" class="done">
</template>
      </el-table-column>
    </el-table>
    <div class="bottom">
      <img src="http://p9lce13x8.bkt.clouddn.com/add.png" class="sys_add" @click="add">
      <img src="http://oqz8dkpuh.bkt.clouddn.com/new.png" class="new">
      <img src="http://oqz8dkpuh.bkt.clouddn.com/quit.png" class="quit"  @click="quit">
    </div>
    </div>
  </div>
</template>

<script>
  import Cookie from '.././cookie.js'
  
  export default {
    data() {
      return {
        username: "biu",
        score: "1000",
        sstaus: 0,
        pstatus: 0,
        tableData: [{
          importance: 3,
          name: '运动',
          hour: '1',
          ddl: '7.21'
        }],
        token: "",
        success: false,
        good: false,
        show: false,
        check: false,
        movie: false,
        done: false
      }
    },
    mounted() {
      this.token = Cookie.getCookie('token');
      this.uid = Cookie.getCookie('uid');
      fetch("/api/user/" + this.uid + "/detal/", {
        method: "GET",
        headers: {
          "token": this.token
        }
      }).then(res => {
        if (res.ok) {
          return res.json();
        }
      }).then(res => {
        this.username = res.username;
        this.score = res.score;
        this.sstaus = res.sstaus;
        this.pstatus = res.pstatus;
        this.time = res.time;
        this.tableData = res.goal;
      })
    },
    methods: {
      back() {
        // this.$router.push("/start")
      },
      quit() {
        this.success = true;
      },
      cancel() {
        this.success = false;
      },
      choice_quit() {
        //退出登陆
        //this.$router.push("/start")
      },
      add() {
        this.show = true;
      },
      no() {
        this.show = false;
      },
      N() {
        this.check = false;
      },
      Y() {
        this.check = false;
        this.movie = true;
      },
      change_yes() {
        let message = {
          importance: this.importance,
          name: this.name,
          hour: this.hour,
          ddl: this.ddl,
          cost: 20
        }
        fetch("/api/user/" + this.uid + row.id + "/exchange/", {
          method: 'POST',
          body: JSON.stringify(message),
          headers: {
            "token": this.token,
          }
        }).then(res => {
          fetch("/api/user/" + this.uid + "/detal/", {
            method: "GET",
            headers: {
              "token": this.token
            }
          }).then(res => {
            if (res.ok) {
              return res.json();
            }
          }).then(res => {
            this.username = res.username;
            this.score = res.score;
            this.sstaus = res.sstaus;
            this.pstatus = res.pstatus;
            this.time = res.time;
            this.tableData = res.goal;
          })
        })
      },
      change_no() {
        this.movie = false;
      },
      yes() {
        let message = {
          importance: this.importance,
          name: this.name,
          hour: this.hour,
          ddl: this.ddl
        }
        fetch("/api/user/" + this.uid + "/addition/", {
          method: 'POST',
          body: JSON.stringify(message),
          headers: {
            "token": this.token,
          }
        }).then(res => {
          if (res.ok) {
            this.gid = res.gid;
          }
        })
      },
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
      finish(index, row) {
        this.good = true;
        this.done = true;
        //cost
        fetch("/api/user/" + this.uid + row.id + "/result/", {
          method: 'POST',
          body: {
            "result": 1
          },
          headers: {
            "token": this.token,
          }
        }).then(res => {
          if (res.ok) {
            fetch("/api/user/" + this.uid + "/detal/", {
              method: "GET",
              headers: {
                "token": this.token
              }
            }).then(res => {
              if (res.ok) {
                return res.json();
              }
            }).then(res => {
              this.username = res.username;
              this.score = res.score;
              this.sstaus = res.sstaus;
              this.pstatus = res.pstatus;
              this.time = res.time;
              this.tableData = res.goal;
            })
          }
        })
      },
      changeRow(index, row) {
        this.check = true;
      },
      deleteRow(index, row) {
        fetch("/api/user/" + this.uid + row.id + "/result/", {
          method: 'DELETE',
          headers: {
            "token": this.token,
          },
          body: {
            "result": 0
          }
        }).then(res => {
          if (res.ok) {
            fetch("/api/user/" + this.uid + "/detal/", {
              method: "GET",
              headers: {
                "token": this.token
              }
            }).then(res => {
              if (res.ok) {
                return res.json();
              }
            }).then(res => {
              this.username = res.username;
              this.score = res.score;
              this.sstaus = res.sstaus;
              this.pstatus = res.pstatus;
              this.time = res.time;
              this.tableData = res.goal;
            })
          }
        })
      },
    }
  }
</script>

<style scoped>
  .top {
    height: 50px;
    width: 100%;
    position: absolute;
    top: 0px;
    left: 0px;
    background-color: #a094a2;
  }
  
  .input {
    background-color: rgb(224, 224, 224);
    width: 90%;
  }
  
  .white {
    background-color: white;
    position: absolute;
    z-index: 5;
    margin: 40% 18%;
    width: 60%;
    height: 50%;
    border-style: solid;
    border-width: 1px;
    border-color: rgb(67, 67, 67);
  }
  
  .button {
    font-size: 20px;
    text-align: center;
    line-height: 20px;
    background-color: rgb(230, 178, 202);
    margin-left: 20px;
    margin-top: 20px;
    width: 70px;
  }
  
  .arrow {
    height: 30px;
    margin-top: 10px;
    margin-left: 20px;
  }
  
  .self {
    margin-left: 7%;
    width: 40%;
    display: inline-block;
  }
  
  .new_title {
    margin-top: 20px;
    margin-left: 23%;
    font-size: 25px;
  }
  
  .new_rask {
    margin-top: 5px;
    margin-left: 10px;
  }
  
  .square {
    display: inline-block;
    border-style: solid;
    border-width: 1px;
    border-color: rgb(67, 67, 67);
    height: 180px;
    width: 30%;
    margin-left: 20px;
    margin-top: 70px;
  }
  
  .girl {
    width: 100%;
    height: 180px;
  }
  
  .id_1 {
    width: 100%;
    height: 30px;
    border-radius: 5px;
    padding: 0px 20px;
    line-height: 30px;
    background-color: #dee2e4;
  }
  
  .id_2 {
    width: 105%;
    height: 30px;
    border-radius: 5px;
    margin-top: 10px;
    padding: 0px 16px;
    background-color: #dee2e4;
  }
  
  .dollar {
    margin-top: 5px;
    width: 20px;
    height: 20px;
  }
  
  .aim {
    margin-top: 3px;
  }
  
  .progress {
    width: 120%;
  }
  
  .time {
    margin-top: 4px;
  }
  
  .sys_add {
    width: 50px;
    height: 50px;
    margin-left: 20px;
  }
  
  .new {
    width: 50px;
    height: 50px;
    margin-left: 25%;
    margin-top: 5px;
  }
  
  .quit {
    width: 50px;
    height: 50px;
    margin-left: 25%;
    margin-top: 5px;
  }
  
  .bottom {
    height: 60px;
    width: 100%;
    position: absolute;
    bottom: 0px;
    left: 0px;
    line-height: 60px;
    background-color: #a094a2;
  }
  
  .quit_choice {
    width: 100px;
    height: 100px;
    position: absolute;
    margin-left: 70%;
    bottom: 60px;
  }
  
  .choicequit {
    position: absolute;
    font-size: 20px;
    bottom: 123px;
    margin-left: 83%;
    color: black;
  }
  
  .cancel {
    position: absolute;
    font-size: 20px;
    bottom: 82px;
    margin-left: 83%;
    color: black;
  }
  
  .black {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
  
  .check_money {
    background-color: white;
    position: absolute;
    z-index: 5;
    margin: 40% 18%;
    width: 50%;
    height: 30%;
    border-style: solid;
    border-width: 1px;
    border-color: rgb(67, 67, 67);
  }
  
  .tip {
    margin-left: 40%;
    margin-top: 20px;
    font-size: 20px;
  }
  
  .contact {
    margin-left: 20px;
    margin-top: 30px;
  }
  
  .button_1 {
    font-size: 20px;
    text-align: center;
    line-height: 20px;
    background-color: rgb(230, 178, 202);
    margin-left: 12px;
    margin-top: 20px;
    width: 70px;
  }
  
  .done {
    width: 20px;
    height: 20px;
    margin-left: 35%;
  }
</style>