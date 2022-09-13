<template>
    <div>
        <p>{{ date_show }} - {{ week }}</p>
        <p>{{ time_show }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            week: '',// 本周周几
            date_show: '', //本日日期
            time_show: '',//当前时间，时分秒
        }
    },
    mounted() {
        // 获取日期-星期
        this.getdataTime()
        // 读秒
        setInterval(() => {
            this.getnewTime()
        }, 1000)
    },
    methods: {
        // 获取当前系统日期
        getdataTime() {
            let wk = new Date().getDay()
            let yy = new Date().getFullYear();
            let mm = new Date().getMonth() + 1;
            let dd = new Date().getDate();
            let weeks = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
            this.week = weeks[wk]
            this.date_show = yy + "年" + mm + "月" + dd + "日"
        },
        // 获取当前系统的时间
        getnewTime() {
            let hh = new Date().getHours();
            let mf =
                new Date().getMinutes() < 10
                    ? "0" + new Date().getMinutes()
                    : new Date().getMinutes();
            let ss =
                new Date().getSeconds() < 10
                    ? "0" + new Date().getSeconds()
                    : new Date().getSeconds();
            this.time_show = hh + ":" + mf + ":" + ss;
        }
    }
}
</script>
