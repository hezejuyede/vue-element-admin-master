<template>
    <div>
        <p>{{ date_show }} {{ week }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            week: '',// 本周周几
            date_show: '', //本日日期
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
        }
    }
}
</script>
