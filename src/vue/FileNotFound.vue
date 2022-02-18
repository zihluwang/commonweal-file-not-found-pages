<template>
  <div class="base-container">
    <div class="wrap_404">
      <div class="wrap_right">
        <div class="list">
          <div class="container toper">
            <h3 id="DM_tips" style="color: #ff0000">ERROR 404</h3>
            <p id="DM_error">该页面找不到或已经被删除了</p>
            <a id="DM_goHomeBtn" target="_blank" style="color: #ff0000;">
              <img src="@/vue/assets/images/logo.png" :height="`18px`" style="vertical-align: middle;" alt="favicon">
              继续浏览
              <span id="DM_timer"></span>
            </a>
          </div>

          <div class="container detail">
            <div class="detail_left">
              <p class="tit">
                <img :src="`${cdnPath}dm.ico`" height="22px"
                     style="vertical-align: sub;" alt="">
                一起寻找走失的儿童
              </p>
              <a target="_blank" :href="child.infoUrl" id="DM_detailLink">
                <img :src="child.photoUrl" class="avatar" id="DM_avatar" alt="">
              </a>
              <p class="md-light">现年<span id="DM_age" style="color: #ff0000;">{{ child.currentAge }}</span>岁，已走失<span
                  id="DM_day" style="color: #ff0000;">{{ child.missingDays }}</span>天。</p>
              <p class="md-light">走失于 <span id="DM_address">{{ child.missingAddress }}</span>。</p>
            </div>
            <div class="detail_right">
              <a id="DM_showDetailBtn" target="_blank" :href="child.infoUrl" style="color: #ff0000;">查看详情
                <el-icon class="el-icon-arrow-right"></el-icon>
              </a>
              <h5 class="detail_title md-light xqzl">
                <img :src="`${cdnPath}d.svg`" class="tb-1" alt="">
                走失信息
              </h5>
              <ul class="detail_list">
                <li>
                <span class="detail_title md-light">
                  <img class="tb" :src="`${cdnPath}icon.svg`" alt="">姓名
                </span>
                  <span class="c_name">{{ child.name }}</span>
                </li>
                <li>
                <span class="detail_title md-light">
                  <img class="tb" :src="`${cdnPath}icon.svg`" alt="">身高
                </span>
                  <span class="c_name">{{ child.height }}</span>
                </li>
                <li>
                <span class="detail_title md-light">
                  <img class="tb" :src="`${cdnPath}icon.svg`" alt="">出生日期
                </span>
                  <span class="c_name">{{ child.bornDate }}</span>
                </li>
                <li>
                <span class="detail_title md-light">
                  <img class="tb" :src="`${cdnPath}icon.svg`" alt="">走失日期
                </span>
                  <span class="c_name">{{ child.missingDate }}</span>
                </li>
                <li>
                <span class="detail_title md-light">
                  <img class="tb" :src="`${cdnPath}icon.svg`" alt="">线索电话
                </span>
                  <span class="c_name">{{ child.contact }}</span>
                </li>
              </ul>

              <h5 class="detail_title md-light dxtz">
                <img :src="`${cdnPath}d.svg`" alt="" class="tb-1">
                典型特征
              </h5>

              <p id="c_description">{{ child.missingDescription }}</p>
              <p class="bq">
                页面分发：
                <a href="https://vorbote.cn" target="_blank">VorBotE开发小组</a>
                <br/>
                数据来源：
                <a href="https://www.dnpw.org/404" target="_blank">域名公益</a>
              </p>

            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {Component, Vue} from 'vue-property-decorator'
import axios from 'axios'
import {Notify} from 'notiflix'

@Component({
  data() {
    return {
      child: {
        bornDate: '',
        contact: '',
        height: '',
        photoUrl: '',
        missingAddress: '',
        missingAge: '',
        missingDate: '',
        missingDays: 0,
        missingDescription: '',
        name: '',
        currentAge: 0,
        infoUrl: '',
        sex: ''
      },
      cdnPath: 'https://cdn.zhaolinlang.com/cdn.dnpw.org/404/res/'
    }
  },
  mounted() {
    axios.get('https://api.zhaolinlang.com/get/num/1').then((res) => {
      const data = res.data['data'][0]
      this.child['bornDate'] = data['born_date']
      this.child['contact'] = data['contact']
      this.child['height'] = data['height']
      this.child['photoUrl'] = data['md_photo']
      this.child['missingAddress'] = data['missing_address']
      this.child['missingAge'] = data['missing_age']
      this.child['missingDate'] = data['missing_date']
      this.child['missingDays'] = data['missing_days']
      this.child['missingDescription'] = data['missing_feature']
      this.child['name'] = data['name']
      this.child['currentAge'] = data['now_age']
      this.child['infoUrl'] = data['url']
      this.child['sex'] = data['sex']

      console.log(this.child)
    }).catch((error) => {
      console.log(error)
      Notify.failure("网络请求失败！")
    })
  },
  methods: {

  }
})
export default class FileNotFound extends Vue {
}
</script>

<style lang="less" scoped>
.base-container {
  margin: 0;
  background-color: #f6f6f6;
  color: #777;
  font-size: 14px;
  background-image: url("~@/assets/images/2kb_bg.png");
  font-family: -apple-system, Helvetica neue, "Pingfang SC", "microsoft yahei", simsun, serif;
  text-align: left;
}

.wrap_404 {
  display: flex;
  align-items: center;
  position: absolute;
  left: 0;
  right: 0;
  min-height: 80vh;
}

.wrap_404 .wrap_right {
  margin: 0 auto;
  border-radius: 5px;
  background-color: #fff;
  overflow: hidden
}

.wrap_404 .wrap_right {
  width: 600px;
  justify-content: flex-start
}

.wrap_404 .wrap_right .list {
  width: 100%
}

.wrap_404 .wrap_right .list .container {
  position: relative;
  margin: 0 24px;
  padding: 12px 0;
  border-bottom: 1px solid #eee
}

.wrap_404 #DM_goHomeBtn, .wrap_404 #DM_showDetailBtn {
  position: absolute;
  top: 20px;
  right: 0
}

#DM_goHomeBtn {
  font-size: 16px
}

.wrap_404 .toper h3 {
  font-size: 40px;
  color: #555;
  width: 82%;
  line-height: 1
}

.wrap_404 .toper p {
  font-size: 25px;
  color: #444
}

.wrap_404 .detail {
  display: flex
}

.wrap_404 .detail .detail_left {
  flex: 4
}

.wrap_404 .detail .detail_left .avatar {
  width: 100%
}

#DM_age, .wrap_404 .detail .detail_left #DM_day {
  font-size: 20px;
  line-height: 1.5
}

.wrap_404 .detail .detail_left #DM_address {
  line-height: 1.2;
  color: #777
}

.wrap_404 .detail .detail_right {
  flex: 6;
  margin: 17px 0 0 17px;
  background: url("~@/assets/images/seal.jpeg") no-repeat right center
}

.wrap_404 .detail .xqzl {
  font-size: 15px;
  margin: 22px 0 10px 0;
  font-weight: 400
}

.wrap_404 .detail .dxtz {
  font-size: 15px;
  margin: 0 0 6px 0;
  font-weight: 400
}

.wrap_404 .red {
  color: #ff3215
}

.wrap_404 .detail .detail_right .detail_title {
  line-height: 0
}

.tb-1, .wrap_404 .detail .detail_right .detail_title .tb {
  margin-right: 5px
}

.wrap_404 .detail .detail_right .detail_list {
  list-style: none;
  padding: 0;
  border-bottom: 1px dashed #efefef
}

.wrap_404 .detail .detail_right .detail_list li {
  display: flex;
  justify-content: space-between;
  line-height: 25px
}

.wrap_404 .dm_children {
  display: flex;
  justify-content: space-around
}

.wrap_404 .dm_children .child_wrap {
  width: 90px;
  text-align: center
}

.wrap_404 .dm_children .child_wrap .avatar {
  width: 100%;
  padding-top: 100%;
  border-radius: 50%;
  border: 1px solid transparent;
  background-position: center;
  background-size: cover;
  cursor: pointer
}

.wrap_404 .tit {
  color: #666;
  font-size: 18px;
  line-height: 30px;
  margin: 0 0 10px 0
}

.wrap_404 .md-light {
  color: #555
}

.wrap_404 .sm-light {
  color: #777
}

.wrap_404 .bq {
  text-align: right;
  color: #999;
  font-size: 12px
}

.wrap_404 .bq a {
  color: #999;
  text-decoration: none
}

.wrap_404 a {
  color: #ff3215;
  cursor: pointer
}

.wrap_404 a:hover {
  color: #0056b3
}

.wrap_404 h3, .wrap_404 p {
  line-height: 1.234;
  margin: 5px;
  padding: 0
}

.wrap_404 .tb {
  width: 18px;
  vertical-align: text-bottom
}

.wrap_404 .tb-1 {
  width: 23px;
  vertical-align: sub
}

#DM_error {
  margin: 10px 5px 0 5px;
}

@media screen and (max-width: 767px) {
  body {
    background-image: unset;
    background: #fff
  }

  .wrap_404 .wrap_right {
    margin-top: 6.66%;
    border-radius: unset
  }

  .wrap_404 .detail {
    display: block
  }

  .wrap_404 .detail .detail_right {
    margin-left: 0
  }

  .wrap_404 .detail .detail_left .avatar {
    display: block;
    width: 95%;
    max-width: 300px;
    margin: 0 auto
  }
}
</style>
