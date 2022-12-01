<template>
  <div>
    <van-image width="100%" height="200" src="https://online-class-1314405309.cos.ap-nanjing.myqcloud.com/2022/11/08/d476e10da2c74d1e9d2e39449fa77fe8203fb80e7bec54e73ee245ceb7389b504ec26ad7.jpg" />
    <van-list v-model="loading" :finished="finished" finished-text="没有更多了">
      <ul class="list">
        <li v-for="(item,index) in list" :key="index">
          <div>
            <h1 class="van-ellipsis">{{ item.courseName }}</h1>
            <span>直播时间：{{ item.startTimeString }}至{{ item.endTimeString }}</span>
            <span>
              直播状态：{{ item.liveStatus == 0 ? '未开始' : item.liveStatus == 1 ? '直播中' : '已结束' }}&nbsp;&nbsp;&nbsp;&nbsp;
              直播老师：{{ item.teacher.name }}
            </span>
          </div>
          <p>
            <button @click="info(item.id)" type="default" size="mini">去看看</button>
          </p>
        </li>
      </ul>

    </van-list>
  </div>
</template>

<script>
import api from '@/api/live'
export default {
  name: "Live",

  data() {
    return {
      list: [],
      loading: false,
      finished: false,
      show: false
    };
  },

  created(){
    this.fetchData();
  },

  methods: {
    fetchData() {
      api.list().then(response => {
        console.log(response.data);
        this.list = response.data;
        this.finished = true;
      });
    },

    info(id) {
      this.$router.push({ path: '/liveInfo/'+id })
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
  li {
    margin: 10px;
    padding-bottom: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #e5e5e5;

    div {
      width: calc(100% - 60px);
      display: flex;
      flex-direction: column;
      h1 {
        font-size: 16px;
      }

      span {
        margin: 0;
        font-size: 12px;
        color: gray;
      }
    }

    p {
      text-align: center;
      color: gray;
      font-size: 12px;
      width: 60px;
    }
  }
}
</style>
