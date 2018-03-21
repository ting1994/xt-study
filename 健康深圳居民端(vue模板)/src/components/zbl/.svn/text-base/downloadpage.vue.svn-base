<template>
<div class="downloadpage" style="overflow-x:hidden;background-color:#F2F2F2;height:100vh;">
    <!-- <div class="header">
        <mt-header title="鹏云健康">
            <a slot="left" @click='$router.go(-1)'>
                <mt-button icon="back"></mt-button>
            </a>
        </mt-header>
    </div> -->
    <div class="body">
        <div class="session-top">
            <div class="bg"></div>
            <div class="container">
                <img src="../../assets/img/1024.png">
                <p class="name">鹏云健康</p>
                <p class="dec">100万次下载<span class="size">20.11MB</span></p>
                <mt-button class="downloadbtn">官网下载<span class="android">(仅安卓)</span></mt-button>
            </div>
        </div>
        <div class="session-down">
            <div class="imgGroup">
                <img src="../../assets/img/imggroup1.png" class="img1">
                <img src="../../assets/img/imggroup3.png" class="img1">
                <img src="../../assets/img/imggroup4.png" class="img1">
            </div>
            <p class="intro">签约家医,就用鹏云健康!</p>
            <p class="andsoon">...</p>
            <p class="version">版本: V1.0</p>
            <p class="updateTime">更新时间： 2017年09月01日</p>
            <div class="iconGroup">
                <div>
                    <img src="../../assets/img/dlicon1.png">无病毒
                </div>
                <div>
                    <img src="../../assets/img/dlicon2.png">无广告
                </div>
                <div>
                    <img src="../../assets/img/dlicon3.png">用户保障
                </div>
            </div>
        </div>
    </div>
</div>
</template>
<script>
import {
    commonAjax,
    commonAjaxKy
} from '../../api/api.js'
export default {
    data: function() {
        return {}
    },
    computed: {},
    components: {},
    methods: {},
    created() {},
    mounted() {}
}
</script>
<style lang='stylus' scoped>
// @font-face {
//     font-family: 'YourWebFontName';
//     src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
//     src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
//         url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
//         url('YourWebFontName.ttf')  format('truetype'), /* Safari, Android, iOS */
//         url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */
//    }
.downloadpage {
  font-family: 'Microsoft Yahei';
}
.body {
    .session-top {
      background: url('../../assets/img/download-bg.png') no-repeat;
      background-size: 100% 100%;
      width: 100%;
      height: 5.2rem;
      position: relative;
      .bg {
        background: url('../../assets/img/download-bg2.png') no-repeat;
        background-size: 100% 100%;
        width: 100%;
        height: 2.5rem;
      }
      .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        position: absolute;
        top: .5rem;
        left: 50%;
        transform: translateX(-50%);
        img {
          width: 1.8rem;
          height: 1.8rem;
        }
        .name {
          margin-top: 15px;
          font-size: .32rem;
          color: #333;
        }
        .dec {
          margin-top: 7px;
          font-size: .24rem;
          color: #999;
          .size {
            margin-left: .38rem;
          }
        }
        .downloadbtn {
          margin-top: 18px;
          background-color: #6aa0ff;
          font-size: .32rem;
          color: #fff;
          width: 5.66rem;
          height: .98rem;
          .android {
            margin-left: 5px;
            font-size: .26rem;
          }
        }
      }
    }
    .session-down {
      // margin: 15px;
      padding: 16px 20px;
      position: relative;
      display: flex;
      flex-direction: column;
      background: url('../../assets/img/download-bg3.png') no-repeat;
      background-size: 100% 100%;
      .imgGroup {
        display: flex;
        flex-direction: row;
        margin-bottom: 15px;
        overflow-x: auto;
        .img1 {
          width: 3.93rem;
          height: 5.13rem;
          margin-right: 16px;
        }
      }
      .intro {
        font-size: .28rem;
        color: #333;
        margin-bottom: 10px;
      }
      .andsoon {
        font-size: .28rem;
        margin-bottom: 12px;
      }
      .version {
        font-size: .24rem;
        color: #666;
        margin-bottom: 9px;
      }
      .updateTime {
        font-size: .24rem;
        color: #666;
        margin-bottom: 20px;
      }
      .iconGroup {
        display: flex;
        flex-direction: row;
        margin-bottom: 10px;
        div {
          margin-right: .41rem;
          display: flex;
          flex-direction: row;
          align-items: center;
          font-size: .22rem;
          color: #999;
          img {
            margin-right: .2rem;
            width: auto;
            height: .32rem;
          }
        }
      }
    }
}
</style>
