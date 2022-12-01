<template>
  <div>
    <van-image width="100%" height="200" src="https://online-class-1314405309.cos.ap-nanjing.myqcloud.com/2022/11/08/d476e10da2c74d1e9d2e39449fa77fe8203fb80e7bec54e73ee245ceb7389b504ec26ad7.jpg" />
    <van-list v-model="loading" :finished="finished" finished-text="没有更多了" @load="onLoad">
      <ul class="list">
        <li v-for="(item,index) in list" :key="index">
          <div>
            <h1 class="van-ellipsis">第一课 大数据算法</h1>
            <span>2022-11-03 11:12:23</span>
          </div>
          <p>
            [回放]
          </p>
        </li>
      </ul>
    </van-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      list: [],
      loading: false,
      finished: false,
    };
  },
  mounted() {
    this.axios
      .get("https://jsonplaceholder.typicode.com/todos/1")
      .then((response) => {
        console.log(response.data);
      });
  },
  methods: {
    onLoad() {
      // 异步更新数据
      // setTimeout 仅做示例，真实场景中一般为 ajax 请求
      setTimeout(() => {
        for (let i = 0; i < 10; i++) {
          const time = new Date().getTime();
          this.list.push({
            id: i,
            title:
              "第一课 大数据技术" +
              i,
            time,
          });
        }
        // 加载状态结束
        this.loading = false;
        // 数据全部加载完成
        if (this.list.length >= 40) {
          this.finished = true;
        }
      }, 1000);
    },
  },
};
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
      color: orangered;
      font-size: 12px;
      width: 60px;
    }
  }
}
</style>