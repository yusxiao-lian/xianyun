<template>
  <div class="index">
    <!-- 轮播 -->
     <el-carousel>
      <el-carousel-item v-for="(item, index) in banner" :key="index">
        <div class="banner" :style="`background:url(${item}) center center no-repeat;`"></div>
      </el-carousel-item> 
    </el-carousel>
    <!-- 搜索框 -->
    <div class="banner-content">
			<div class="search-bar">
				<!-- tab栏 -->
				<el-row type="flex" class="search-tab">
					<span v-for="(item, index) in options"
          :key="index" @click="handleClick(index)" :class="{active: index===current}">
						<i>{{item.title}}</i>
					</span>
				</el-row>

				<!-- 输入框 -->
				<el-row type="flex" align="middle" class="search-input">
					<input
						:placeholder="options[current].placeholder"
					/>
					<i class="el-icon-search"></i>
				</el-row>
			</div>
		</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: 0,
      banner: [
        'http://157.122.54.189:9095/assets/images/th01.jfif',
        'http://157.122.54.189:9095/assets/images/th02.jfif',
        'http://157.122.54.189:9095/assets/images/th03.jfif'
      ],
      options: [
        {title: '攻略', placeholder: '搜索城市'},
        {title: '酒店', placeholder: '请输入城市搜索酒店'},
        {title: '机票', placeholder: '搜索城市'}
      ]
    }
  },
  methods: {
    handleClick (index) {
      this.current = index
      if (index === 2) {
        this.$router.push({ path: '/air' })
      }
    }
  },
  mounted () {
    this.$axios({
      url: '/scenics/banners'
    }).then((res) => {
      console.log(res)
    })
  }
}
</script>

<style lang='less' scoped>
.index {
  height: 700px;
  min-width: 1000px;
  .banner {
    width: 100%;
    position: absolute;
    height: 700px;
  }
  /deep/.el-carousel__container {
    height: 700px;
    min-width: 1000px;
  }
  .banner-content{
    z-index:9;
    width:1000px;
    position:absolute;
    left:50%;
    top:45%;
    margin-left: -500px;
    border-top:1px transparent solid;

    .search-bar{
        width:552px;
        margin:0 auto;
    }

    .search-tab{
        .active{
            i{
            color:#333;
            }
            &::after{
            background: #eee;
            }
        }

        span{
            width:82px;
            height:36px;
            display:block;
            position: relative;
            margin-right:8px;
            cursor: pointer;

            i{
            position:absolute;
            z-index:2;
            display: block;
            width:100%;
            height:100%;
            line-height:30px;
            text-align:center;
            color:#fff;
            }

            &:after{
            position: absolute;
            left:0;
            top:0;
            display:block;
            content: "";
            width:100%;
            height:100%;
            border: 1px rgba(255,255,255,.2) solid;
            border-bottom: none;
            transform: scale(1.1,1.3) perspective(.7em) rotateX(2.2deg);
            transform-origin: bottom left;
            background: rgba(0,0,0,.5);
            border-radius:1px 2px 0 0;
            box-sizing:border-box;
            }
        }
    }

    .search-input{
        width:550px;
        height:46px;
        background:#fff;
        border-radius: 0 4px 4px 4px;
        border: 1px rgba(255,255,255,.2) solid;
        border-top:none;
        box-sizing: unset;

        input{
            flex:1;
            height:20px;
            padding: 13px 15px;
            outline: none;
            border:0;
            font-size:16px;
        }

        .el-icon-search{
            cursor :pointer;
            font-size:22px;
            padding:0 10px;
            font-weight:bold;
        }
    }
  }
}
</style>