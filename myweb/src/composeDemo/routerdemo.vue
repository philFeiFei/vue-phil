<template>
    <div>
        <h3>this is the main outer app 类似app.vue </h3>

        <router-view></router-view>

    </div>
</template>
<script>
import login from "../components/login.vue";
import c_vuex from "../components/vuexTest.vue";
export default {
    methods: {
        showDetail(uid) {
            // this.$router.push({ path: "/player/" + uid.toString() });
            this.$router.push({
                path: "/player/" + uid.toString()
            });
        }
    },
    components: {
        login,
        c_vuex
    }
};
</script>


