<template>
  <div class="moving">
    <div class="tit">
      <h1>电影票 - {{city}}</h1>
      <div id="" class="locat">
        <el-dropdown trigger="click" @command="changeCity">
            <span class="el-dropdown-link">
              [切换城市]
            </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item v-for="(city,index) in citys" :command="city.name" :key="index">{{city.name}}</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
      <div class="hd">
        <h2>影院上映</h2>
        <ul class="tab-hd clearfix">
          <li class="on">正在上映</li>
        </ul>
      </div>
    </div>
    <div class="content-container">
      <MoviesTag :data="this.movingData"></MoviesTag>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import MoviesTag from './common/moviesTag.vue'
export default {
  name: 'movie',
  data () {
    return {
      citys: [
        {
          name: '北京'
        },
        {
          name: '上海'
        },
        {
          name: '广州'
        },
        {
          name: '深圳'
        },
        {
          name: '杭州'
        }
      ]
    }
  },
  mounted () {
    this.$store.commit('MOVING_LOADING', {loading: true})
    this.$store.dispatch('getMoving')
  },
  methods: {
    changeCity(command) {
      this.$store.commit('MOVING_LOADING', {loading: true})
      this.$store.commit('MOVIE_CITY', {city: command})
      this.$store.dispatch('getMoving')
    }
  },
  components: {
    MoviesTag
  },
  computed: {
    ...mapGetters([
      'movingData',
      'city'
    ])
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
@import "../../style/color";
@import "../../style/base";
.moving {
  margin-bottom: 20px;
  p {
    color: red;
  }
  .tit {
    width: 950px;
    margin: 0 auto;
    margin-top: 20px;
    h1 {
      display: inline-block;
      width: 126px;
      font-size: 20px;
      color: #000;
    }
    .locat {
      position: relative;
      display: inline-block;
    }
    .hd{
      border: none;
      margin: 15px 0;
    }
  }
  .content-container{
    width: 950px;
    overflow: hidden;
    margin: 10px auto;
    padding-bottom: 20px;
  }
}
</style>
