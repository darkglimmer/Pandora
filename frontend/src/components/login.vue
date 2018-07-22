<template>
    <div class="container">
        <div class="mask"></div>

        <div class="dialog">
            <div class="title"  >欢迎回来，勇者！</div>
            <div class="content">
                <div class="l40 pt15">
                    <input class="dialog-input username" type="input" placeholder="用户名" v-model="account"/>
                </div>
                <div class="l40 pt15">
                    <input class="dialog-input password" type="input" placeholder="密码" v-model="password"/>
                </div>
                <div>
                    <div class="submit " @click = "login()" >登录</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Cookie from '.././cookie.js'

    export default {
        data() {
            return {
                form: {
                    username: "",
                    password: ""
                }
            };
        },
        methods: {
            login() {
                this.$router.push("/main")
                let message = {
                    username: this.form.username,
                    password: this.form.password
                };
                Cookie.setCookie('url', window.location.href);
                fetch("/api/signin/", {
                    method: 'POST',
                    body: JSON.stringify(message),
                }).then(res => {
                    if (res.ok) {
                        return res.json();
                    }
                }).then(res => {
                    Cookie.setCookie("uid", res.uid)
                    Cookie.setCookie("token", res.token)
                    this.$router.push("/main")
                })
            }
        },
    }
</script>

<style>
    @import '../assets/reset.css';
    .but {
        width:200px;
        margin: 0 auto;
        display: block;
        background: white;
        z-index: 9000;
    }
    .line{
        margin-top: 10px;
        /* width: 300px; */
    }
    .login{
        width:100px;
    }
    .container{
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
</style>