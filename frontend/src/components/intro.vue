<template>
    <div class="parent">
        <div class="mask" v-if = "flag"></div>
        <img src="http://p9lce13x8.bkt.clouddn.com/older.png" class="npc"/>
        <div id="text" @click = "next()">
            {{txt[index]}}
            <img src="http://p9lce13x8.bkt.clouddn.com/right.png" class="arrow"/>
        </div>

        <div class="dialog" v-if = "flag">
            <div class="title"  >注册成为勇者吧！</div>
            <div class="content">
                <div class="l40 pt15">
                    <input class="dialog-input username" type="input" placeholder="用户名" v-model="account"/>
                </div>
                <div class="l40 pt15">
                    <input class="dialog-input password" type="input" placeholder="密码" v-model="password"/>
                </div>
                <div>
                    <div class="submit " @click = "login()" >注册</div>
                </div>
            </div>
        </div> 
    </div>
</template>

<script>
export default {
    name: 'intro',
    data () {
        return{
            txt:[
                "你好，勇者大人。欢迎来到潘多拉的世界。",
                "作为村长，很高兴能够看到你这样的年轻人来到这里消灭罪恶。说起来，还没问过你的名字和一些基本信息呢！",
                "",
                "不错的名字！为了计算打败罪恶的多少，每位勇者都会设定自己的密匙，要牢牢记住自己的密匙哦！",
                "好啦，寒暄就到此为止，选择潘多拉魔盒中的恶习，用你坚定的意志打败他们吧，成为世界第一的勇者大人吧！"

            ],
            index: 0,
            flag: false,
            account: "",
            password: "",
        }
    },
    mounted(){
        // var str = this.txt[this.index];
        // var i = 1;
        // var bound = document.getElementById("text");
          
        // function feed(){
        //       if(i == str.length+1){
        //           this.index++;
        //           if(this.index > this.txt.length){
        //               console.log("!");
        //               this.index = 0;
        //           }
        //           bound.innerText = ' ';
        //           str = this.txt[this.index];
        //           i = 0;
        //       }
        //       bound.innerText == str.substring(0, i);
        //       i++;
        //       setTimeout("feed()", 200);
              
        // }
    },
    methods: {
        next(){
            if(this.flag == false){
                this.index++;
            }
            if(this.index == 2){
                // this.$options.methods.change();
                this.flag = !this.flag;
            } else if(this.index == 4){
                this.$router.push("/choose");
            }
            
            // if(this.index == 2){
            //     this.$options.methods.sign_ac();
            // } else if(this.index == 3){
            //     this.$options.methods.sign_pw();
            // }else if(this.index == 4){
            //     this.$router.push("/choose");

            // }
                        
        },
        // sign_ac(){
        //     this.account = prompt("请输入您的用户名","");

        // },
        // sign_pw(){
        //     this.password = prompt("请输入您的密码","");
        // },
        login(){
          if(this.username == ""|| this.password=="" ){
              alert("用户名或密码不能为空！");
          }
        //   var data = {
        //       "username": this.username,
        //       "password": this.password,
        //   };
        //   fetch("/api/signup/", {
        //       method: 'POST',
        //       body:  JSON.stringify(data),
        //       headers: {
        //         "token": "eyJhbGciOiJIUzI1NiJ9.eyJpZCI6ODF9.2qVoAYnT-cwHr1eJdXc_u8FrhlfFTbQSrB-JVizHf5w" ,
        //         "Content-Type":"application/json"   
        //       }
        //   }).then(res => {
        //       if (res.ok) {
		//         return res.json()
        //       } else {
        //           console.log('x');
        //         this.failed = true;
	    //       }
        //     }).then(res => {
        //        if(res.message == 0){
        //             alert("用户名已存在！");
        //        } else {
                
        //             this.flag = !this.flag;
        //             this.index++;
        //        }
                
        //     })

            this.flag = !this.flag;
            this.index++;
        }

      
    }
}
</script>

<style scoped>
.parent{
    background-image: url(http://p9lce13x8.bkt.clouddn.com/newbg.png);
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
.npc{
    width: 250px;
    padding-top: 50%;
}
#text{
    background-image: url(http://p9lce13x8.bkt.clouddn.com/talk.png);
    background-repeat: no-repeat;
    background-size: contain ;
    text-align: left;
    width: 380px;
    height: 180px;
    position: absolute;
    bottom: 0;
    padding: 50px 50px;
    box-sizing: border-box;
    font-size: 16px;
    
}
.arrow{
    width:30px;
    margin-left: 5px;
    animation: move 0.8s infinite;
}

.dialog{
    width: 300px;
    height: 280px;
    /* display: none; */
    position: absolute;
    top: 30%;
    left: 30px;
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
.pt15{
    /* padding-top: 15px; */
}
.l40{
    margin-top: 15px;
    height: 40px;
    line-height: 40px;
    text-align: right;
}
.dialog-input{
    width: 100%;
    height: 40px;
    margin: 0px;
    padding:0px;
    border: 1px solid #d5d5d5;
    font-size: 16px;
    color: black;
    text-indent: 25px;
    outline: none;
}

.submit{
    width: 100%;
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
    margin-top: 25px;
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

@keyframes move {
    from {margin-left: 0px;}
}

</style>
