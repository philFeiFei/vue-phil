<template>
    <div class="player">
        <p>您好，测试。你访问了./player/{{detail.uid}}</p>
        <br>
        <p>player详细信息：{{detail.uid}}--{{detail.name}}--{{detail.point}}--{{detail.status}}</p>
        <router-link :to="status">目前状态</router-link>
        <router-link :to="profile">简介</router-link>
        <hr>
        <router-view></router-view>
    </div>
</template>
<style scoped>
.player {
  width: 400px;
  height: 300px;
  border: 1px solid thistle;
  left: 40%;
  position: relative;
}
</style>

<script>
import { Message } from "element-ui"
export default {
    name: "player",
    data() {
        return {
            detail: {},
            status: "",
            profile: ""
        };
    },
    created() {
        Message.info("player vue created!!!!");
    },
    mounted() {
        this.detail = this.getPlayer(this.$route.params.uid);
        this.status = "/player/" + this.$route.params.uid + "/status";
        this.profile = "/player/" + this.$route.params.uid + "/profile";
    },
    //这个是路由url地址切换是例如从play/1跳转至player/2，会触发
    beforeRouteUpdate(to, from, next) {
        console.log("player--beforeRouteUpdate");
        this.detail = this.getPlayer(to.params.uid);
        this.status = "/player/" + to.params.uid + "/status";
        this.profile = "/player/" + to.params.uid + "/profile";
        next();
    },
    beforeRouteEnter(to, from, next) {
        console.log("player--beforeRouteEnter");
        next();
    },
    beforeRouteLeave(to, from, next) {
        console.log("player--beforeRouteLeave");
        this.$notify({
            title: '成功',
            message: '这是一条成功的提示消息',
            type: 'success'
        });
        this.$message("即将离开了player组件");
        if (global.confirm("are you sure leave this component-player?")) {
            next();
        }
    },
    methods: {
        getPlayer(uid) {
            switch (uid) {
                case "1":
                    return {
                        uid: 1,
                        name: "科比",
                        point: 81,
                        profile:
                            "我是科比，你们都懂的，我打球是牛逼的，无法超越的你懂的吧。不说了。我有三个女儿",
                        status: "我已经退役两年了！！！"
                    };
                case "2":
                    return {
                        uid: 2,
                        name: "詹姆斯",
                        point: 60,
                        profile:
                            "我是詹姆斯，你们都懂的，我有儿子，我搬到了洛杉矶，我要投资商业了。你懂得！",
                        status: "我目前仍然是nba第一人！！！"
                    };
                case "3":
                    return {
                        uid: 3,
                        name: "迈克尔乔丹aj",
                        point: 56,
                        profile:
                            "我是Jordan，你们都懂的，我的各种产品，每年获得的利润无数。",
                        status: "我退役了。但我是神！！！"
                    };
                case "4":
                    return {
                        uid: 4,
                        name: "欧文四代aj战靴",
                        point: 33,
                        profile: "我是欧文，你们的德鲁大叔，你们懂得，运球我是最牛逼的。",
                        status: "新赛季王者归来。但我是神！！！"
                    };
                default:
                    return {
                        uid: -1
                    };
            }
        }
    }
};
</script>


<style scoped>
//scoped 表示只对当前模版生效。
p {
  color: red;
}
</style>





