<template>
<div class="app" style="overflow-x:hidden;height:100vh;background-color: #fafafa;">
    <div class="header">
        <mt-header title="咨询记录">
            <a slot="left" @click="$router.push('#')">
                <mt-button icon="back"></mt-button>
            </a>
        </mt-header>
    </div>
    <div class="session">
        <ul class="consultStatus cbafter bgFFF">
            <li v-for="(item,index) in navbarName" :class='index==0?"selected":""' @click="selectTag(index,item)">{{item}}</li>
        </ul>
        <ul class="consultList bgFFF">
            <li class="cbafter" v-for="(item,index) in consultRecord">
                <img v-if="item.avatarId=='0'" class="fl" src="../../assets/img/zy_doctor2.png">
                <img v-else class="fl" :src="imgUrl+item.avatarId">
                <div class="consultCon fl">
                    <p class="docName">{{item.displayName}} 
                        <em v-if="item.status=='01'" class="consultStatus" style="background: #f9ca08">待回复</em>
                        <em v-if="item.status=='02'" class="consultStatus" style="background: #67cc70">已回复</em>
                        <em v-if="item.status=='08'" class="consultStatus" style="background: #e3e3e3">已结束</em>
                        <span class="consultTime">{{item.dispayTime}}</span>
                    </p>
                    <span class="consultDetail">{{item.displayText}}</span>
                </div>
            </li>
        </ul>
        <div id="more" v-if="consultRecord.length>=20" class="more bgFFF" @click="showMore()">查看更多</div>
    </div>
</div>
</template>
<script>
import md5 from 'md5'
import {
    commonAjax,
    requestLoginon,
    areaAjax,
    dicAjax,
    commonAjaxKy
} from '../../api/api.js'
import {
    Navbar, TabItem
} from 'mint-ui'
import {
    mapState,
    mapActions
} from 'vuex'
export default {
    data() {
        return {
            navbarName: ["全部","待回复","已回复","已结束"],
            pageSize: 20,
            pageNo: 1,
            status: '',
            imgUrl: 'http://122.224.131.235:9088/hcn-web/upload/',
            consultRecord: []
        }
    },
    methods: {
    	showMore(){
    		var consultUl = document.querySelector('.consultList')
            this.pageNo++
            let params = [{"pageSize":this.pageSize,"targetId":JSON.parse(sessionStorage.getItem('userInfoDetail')).mpiId,"status":this.status,"targetType":"041","pageNo":this.pageNo}]
            commonAjax(params, 'pcn.imChatService', 'qryTargetData')
            .then(res => {
                if (res.code === 200) {
                	console.log(res.body)
                    this.consultRecord = this.consultRecord.concat(res.body.rows)
           	 		consultUl.style.display = 'block'
           	 		if(res.body < 10){
                        document.getElementById('more').style.display = 'none'
                    }
                }
            })
        },
        selectTag(index,item){
            var navbarList = document.querySelectorAll('.consultStatus li')
            var consultUl = document.querySelector('.consultList')
            
            if(item=='已回复'){
                this.status='02'
            }else if(item=='待回复'){
                this.status='01'
            }else if(item=='已结束'){
                this.status='08'
            }else{
            	this.status=''
            }
            for(var i=0;i<navbarList.length;i++){
                navbarList[i].classList.remove('selected')
                consultUl.style.display = 'none'
            }
            navbarList[index].classList.add('selected')
            let params = [{"pageSize":this.pageSize,"targetId":JSON.parse(sessionStorage.getItem('userInfoDetail')).mpiId,"status":this.status,"targetType":"041","pageNo":this.pageNo}]
            commonAjax(params, 'pcn.imChatService', 'qryTargetData')
            .then(res => {
                if (res.code === 200) {
                    this.consultRecord = res.body.rows
           	 		consultUl.style.display = 'block'
                }
            })
        }
    },
    mounted() {
        let params = [{"pageSize":this.pageSize,"targetId":JSON.parse(sessionStorage.getItem('userInfoDetail')).mpiId,"status":this.status,"targetType":"041","pageNo":this.pageNo}]
        commonAjax(params, 'pcn.imChatService', 'qryTargetData')
        .then(res => {
            if (res.code === 200) {
                this.consultRecord = res.body.rows
//              console.log(this.consultRecord)
            }
        })
    }
}
</script>

<style lang='stylus' scoped>
mainColor = #35B46F
greyFont = #ADADAD
fontSize = .4rem
.header {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    .mint-header {
        height: 1rem;
        font-size: fontSize;
        background-color: mainColor;
    }
}
.bgFFF{background-color: #fff;}
.session {
    margin-top: 1rem;
    .consultStatus{
        li{
            float: left;
            width: 25%;
            text-align: center;
            font-size: .3rem;
            color: #989898;
            padding: .3rem 0;
        }
        .selected{
            color: #3fb97c;
            border-bottom: 2px solid #35b46f;
        }
    }
    .consultList{
        li{
            padding: .3rem;
            border-top: 1px solid #e4e4e4;
            img{
                width: 15%;
                height: 15%;
                border-radius: 50%;
            }
            .consultCon{margin-left: 5%;width: 80%;}
            .docName{
                margin-bottom: .2rem;
                font-size: .4rem;
                .consultStatus{
                    display: inline-block;
                    padding: .1rem .2rem;
                    color: #fff;
                    font-size: .2rem;
                    border-radius: .3rem;
                }
                .consultTime{
                    float: right;
                    font-size: .3rem;
                    color: #9f9f9f;
                    margin-top: .06rem;
                }
            }
            .consultDetail{
                line-height: .4rem;
                font-size: .3rem;
                color: #9f9f9f;
                overflow: hidden;
                text-overflow: ellipsis;
                display: -webkit-box;
                -webkit-line-clamp: 2;
                -webkit-box-orient: vertical;
            }
        }
    }
}
.session .more{
    font-size: .2rem;
    text-align: center;
    padding-bottom: 10px;
}
</style>
