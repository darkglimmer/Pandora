<template>
    <div class="container">
            <div class="">your name:</div>
            <input v-model="form.username"></input>
            <div class="密码:">your password：</div>
            <input v-model="form.password"></input>
            <button class="login" @click="login">开启你的旅程</button>
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
    .login {
        margin: 0 auto;
        display: block;
    }
    
    .container {
        display: flex;
        justify-content: center;
        padding: 100px;
    }
</style>