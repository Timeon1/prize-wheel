<template>
  <div class="wrap-home">

    <div class="wheel-wrap">

      <div class="wheel-wrapper">
        <div
          class="wheel-pointer"
          @click="onClickRotate"
        >
          <!-- Start -->
        </div>
        <div
          class="wheel-bg"
          :class="{freeze: freeze}"
          :style="`transform: rotate(${wheelDeg}deg)`"
        >
          <div class="prize-list">
            <div
              class="prize-item-wrapper"
              v-for="(item,index) in prizeList"
              :key="index"
            >
              <div
                class="prize-item"
                :style="`transform: rotate(${(360/ prizeList.length) * index}deg)`"
              >
                <div class="prize-name">
                  {{ item.name }}
                </div>
                <div class="prize-icon">
                  <img :src="item.icon">
                  <!-- <div class="bgimg"></div> -->

                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  <!-- </div> -->


  </div>
</template>

<script>


export default {
  data() {
    return {
      freeze: false,
      rolling: false,
      wheelDeg: 0,
      prizeNumber: 6,
      prizeListOrigin: [
        {
          icon: "/static/imgs/prizeImg/cp_rgm.png",
          name: "蔡林记热干面"
        },
        {
          icon: "/static/imgs/prizeImg/cp_yb.png",
          name: "周黑鸭"
        },
                {
          icon: "../static/imgs/prizeImg/cp_nrm.png",
          name: "襄阳牛杂面"
        },
        {
          icon: "/static/imgs/prizeImg/cp_of.png",
          name: "洪湖藕粉"
        },
                {
          icon: "/static/imgs/prizeImg/cp_xg.png",
          name: "襄阳牛肉面"
        },
        {
          icon: "/static/imgs/prizeImg/cp_xl.png",
          name: "谢谢参与"
        },
      ],

    };
  },
  components:{
  },
  watch: {
    prizeNumber () {
      this.freeze = true
      this.wheelDeg = 0
     
      setTimeout(() => {
         this.freeze = false
      }, 0)
    },

  },
  created(){

  },

  computed: {
    prizeList () {
      return this.prizeListOrigin.slice(0, this.prizeNumber)
    },

  },
  methods:{

    async onClickRotate() {
 
      if (this.rolling) {
        return;
      }
      this.rolling = true;
      const { wheelDeg, prizeList } = this;
      const random = Math.floor(Math.random() * (prizeList.length ));

      this.wheelDeg =
        wheelDeg -
        wheelDeg % 360 +
        6 * 360 +
        (360 - 360 / prizeList.length * random);

      setTimeout(() => {
        this.rolling = false;
        alert("Result：" + prizeList[random].name);

      }, 4500);
    },


  },

};
</script>

<style scoped lang="less">

body {
  background: #e5f8fe;
}

button {
  border: 0;
  background-color: transparent;
  outline: none;
}
.wrap-home {
  width: 100%;
  height: 100vh;
  background: #e5f8fe;
  background-position: bottom center;
  background-color: #e5f8fe;
  background-size: 750px 240px;
  background-repeat: no-repeat;
}
.wheel-wrap {
  height: 850px;
  background-position: top center;
  background-repeat: no-repeat;
  background-size: 560px 200px;
}
.wheel-wrapper {
    width: 600px;
    height: 600px;
    position: absolute;
    top: 250px;
    left: 50%;
    transform: translateX(-50%);
  }

  .wheel-pointer {
    width: 200px;
    height: 200px;
    border-radius: 1000px;
    background: transparent;
    background-image: url('../../static/imgs/zp_zx.png');
    background-size: 200px 200px;
    background-position: center;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    line-height: 60px;
    z-index: 10;
  }
  .pointer-disabled {
    background-image: url('../../static/imgs/zp_zxdis.png');
  }
  .wheel-bg {
    width: 100%;
    height: 100%;
    border-radius: 1000px;
    overflow: hidden;
    transition: transform 4s ease-in-out;
    // background: #7EEF97;
    &.freeze {
      transition: none;
      background: red;
    }
  }

  .prize-list {
    width: 100%;
    height: 100%;
    position: relative;
    text-align: center;
    background-image: url('../../static/imgs/zp_bg.png');
    background-position: center;
    background-size: 600px 600px;
  }

  .prize-item-wrapper {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 300px;
    height: 300px;
    &:first-child {
      // background-color: pink;
    }

  }

  .prize-item {
    width: 100%;
    height: 100%;
    transform-origin: bottom;

    .prize-name {
      padding: 16px 0;
      padding-top: 50px;
    }

    .prize-icon {
      img {
        width: 120px;
        height: 100px;
      }
        

      // display: flex;
      // justify-content: center;
      // .bgimg {
      //   width: 120px;
      //   height: 120px;
      //   background-image: url('../../static/imgs/prizeImg/cp_xg.png');
      //   background-repeat: no-repeat;
      //   background-size: 120px;
      //   background-position: center;

      // }
    }
  }

    .seamless-warp {
        height: 284px;
        overflow: hidden;
    }

  .board {
    width: 100%;
    // position: absolute;
    // bottom: 10px;
    // left: 50%;
    // transform: translateX(-50%);
    padding: 0 46px;
    box-sizing: border-box;
    .bord-content {
      height: 284px;
      background-color: #ffffff;
      border: 18px solid #0ccb95;
      box-sizing: border-box;
      border-radius: 10px;
      overflow: hidden;
      padding: 0 28px;
      
      .bord-scroll {
        min-height: 284px;
        // animation: 9s boardscroll linear infinite normal;
        // -webkit-animation: 9s boardscroll linear infinite normal;
        // position: relative;
        // -webkit-backface-visibility: hidden;
        // -webkit-transform-style: preserve-3d;
      }
      .content-item {
        width: 100%;
        height: 60px;
        line-height: 60px;
        display: flex;
        justify-content: space-between;
        font-size: 22px;
        & div:first-child,
        & div:nth-child(3)  {
          color: #7d562d;
        }
        & div:nth-child(2) {
          color: #03b482;
        }
      }

    }
  }

  // @keyframes boardscroll {
    
  //   0% {
  //       -webkit-transform: translate3d(0, 0, 0);
  //       transform: translate3d(0, 0, 0);
  //   }
  //   100% {
  //       -webkit-transform: translate3d(0, -600px, 0);
  //       transform: translate3d(0, -600px, 0);
  //   }
  // }
  @keyframes bordscrollT {
    0% {
      transform: translateY(284px);
    }
    100% {
      transform: translateY(-284px);
    }

    
    // 0% {
    //     -webkit-transform: translate3d(0, -284px, 0);
    //     transform: translate3d(0, -284px, 0);
    // }
    // 100% {
    //     -webkit-transform: translate3d(0, -0, 0);
    //     transform: translate3d(0, 0, 0);
    // }
  }


.s-tabs-content-head {
  height: 20px;
  position: relative;
  .content-head-tits {
    width: 110px;
    height: 20px;
    background-color: #0ccb95;
    border-radius: 10px 10px 0 0;
    position: absolute;
    top: 0;
    left: 40px;
  }
}

   .rule-btn-b {
     top: 118px;
   }
</style>
