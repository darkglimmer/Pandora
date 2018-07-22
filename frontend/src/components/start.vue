<template>
    <div class="parent">
        <img src="http://p9lce13x8.bkt.clouddn.com/title.png" class="title" />
        <img src="http://p9lce13x8.bkt.clouddn.com/box.png" class="box"/> 
        <div class="ellipse"></div>
        <button class="but " @click="start">START</button>
        <button class="but " @click="conti">CONTINUE</button>
    </div>
</template>

<script>
export default {
    name: 'start',
    data () {
        return{

        }
    },
    methods: {
        start(){
            this.$router.push("/intro")
        },
        conti(){
            this.$router.push("/login")
        }
        
    }
}
</script>

<style scoped>

.parent{
    background-image: url(http://p9lce13x8.bkt.clouddn.com/bg.png);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    width: 100%;
    height: 100%;
    min-height: 667px;
    display: block;
    position: absolute;
    top:0;
    left:0;
    text-align: center
}
.title{
    margin: 70px auto;
    width:320px;
}
.but{
    width: 120px;
    height: 40px;
    background: #f3f12a;
    font-size: 18px;
    color: #666666;
    border-width: 0;
	border-radius: 5px; 
    outline: none;
    margin:10px;
    vertical-align: middle;
}
.but:hover{
    background: #f3f02a;
    color: #c5c5c5;
}
.box{
    width: 270px;
}
.ellipse{
  width: 150px;
  height: 15px;
  margin: 10px auto;
  background: #c5c5c5;
  border-radius: 50% / 50%;
}


</style>
