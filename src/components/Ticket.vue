<template>
  <div class="ticket-wrap">
    <h2 style="padding-left: 10px; text-align: left">待处理工单</h2>
    <div class="infinite-list-wrapper" style="overflow:auto">
      <ul
        class="list"
        v-infinite-scroll="load"
        infinite-scroll-disabled="disabled"
        style="list-style-type: none;padding-inline-start: 0px">
        <li v-for="(list) in lists" v-bind:key="list.id">
          <div class="ticketShow">
            <el-row>
              <el-card :body-style="{ padding: '0px' }" shadow="hover">
                <img :src=list.image class="image">
                <div class="label">
                  <div style="padding: 5px">
                    <el-link :underline="false" style="font-size: 16px">{{list.title}}</el-link>
                    <time class="time">{{list.time}}</time>
                  </div>
                  <div class="position">{{list.address}}</div>
                  <div class="buttongroup">
                    <el-button class="button" type="primary" v-on:click="view(list.id)">查看</el-button>
                    <el-button class="button" type="success" plain v-on:click="append(list.id)">附加</el-button>
                  </div>
                </div>
              </el-card>
            </el-row>
          </div>
        </li>
      </ul>
      <p v-if="loading" style="color: #2c3e50">加载中...</p>
      <p v-if="noMore" style="color: #2c3e50">没有更多了</p>
    </div>
  </div>
</template>

<style scoped>
  .time {
    font-size: 13px;
    color: #999;
    text-align: right;
    float: right;
  }

  .position {
    padding: 5px;
    font-size: 13px;
    color: #999;
  }

  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .buttongroup {
    margin-top: 15px;
  }

  .el-button {
    float: right;
    margin: 10px;
    width: auto;
  }

  .image {
    height: 120px;
    display: inline-block;
    float: left;
    width: 120px;
    padding: 15px;
  }

  .label {
    padding: 14px;
    text-align: left;
    margin-left: 150px;
  }

  .el-card {
    height: 150px;
    margin: 5px;
  }

</style>

<script>
export default {
  data () {
    return {
      name: 'OrderView',
      id: 1,
      count: 0,
      total: 0,
      loading: false,
      currentDate: new Date(),
      lists: []
    }
  },
  mounted () {
    // get total here
    this.total = 37
  },
  computed: {
    noMore () {
      return this.count >= this.total
    },
    disabled () {
      return this.loading || this.noMore
    }
  },
  methods: {
    load () {
      this.loading = true
      setTimeout(() => {
        for (let i = 0; i < 10; i++) {
          if (this.count >= this.total) {
            break
          }
          // get order information here
          this.lists.push({
            id: this.id,
            image: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
            title: '测试数据' + this.id++,
            time: '2019年8月25日 10:51',
            address: '北京市海淀区学院路37号'
          })
          this.count++
        }
        this.loading = false
      }, 2000)
    },
    view (id) {
      alert('Clicked \'view\' on room id ' + id)
    },
    append (id) {
      alert('Clicked \'append\' on room id ' + id)
    }
  }
}
</script>
