<template>
  <div class="portrait-popup">
    <el-popover popper-class="portrait-popup__wrapper"
                placement="bottom"
                trigger="hover">
      <div class="portrait-popup__container">
        <div class="portrait-popup__info">
          <div class="portrait-flex row align-center">
            <div class="portrait-flex-s">
              <div class="portrait-popup__info--icon">
                <img :src="badgeLevel.iconTie"
                     alt="icon-tie" />
              </div>
            </div>
            <div class="portrait-flex-l">
              <div class="portrait-popup__info--content">
                <div class="portrait-flex row align-center">
                  <div class="portrait-flex-l">
                    <dl>
                      <dt>勋章等级:</dt>
                      <dd>{{ badgeLevel.name }}勋章</dd>
                    </dl>
                    <dl>
                      <dt>个人积分:</dt>
                      <dd>{{ userInfo.points }}</dd>
                    </dl>
                  </div>
                  <div class="portrait-flex-s">
                    <a>如何获得积分<i class="el-icon-arrow-right"></i></a>
                  </div>
                </div>
                <p v-if="lastLevel">
                  您距离晋级
                  <span>{{ lastLevel.name }}勋章</span>
                  还差
                  <span>{{ lastLevel.minPoints - userInfo.points }}分</span>
                  还请再接再厉哦~
                </p>
                <p v-else>您当前已是最高等级~</p>
              </div>
            </div>
          </div>
          <div class="portrait-popup__progress">
            <div class="portrait-popup__progress--bar">
              <span :style=" {width: getProgress() }"></span>
            </div>
            <div class="portrait-popup__progress--list">
              <dl v-for="badge in badges"
                  :key="badge.id"
                  :style="{ left: getPosition(badge) }"
                  :class="{ active: isPositionActive(badge) }"
                  class="portrait-popup__progress--item">
                <dd>{{ badge.minPoints }}</dd>
                <dt>{{ badge.name }}</dt>
              </dl>
            </div>
          </div>
          <img class="portrait-popup__info--bg"
               src="./images/popup-bg.png"
               alt="bg" />
        </div>
        <div class="portrait-popup__details">
          <el-collapse v-model="activeCollapse">
            <el-collapse-item title="一致性 Consistency"
                              name="1">
              <div slot="title"
                   class="portrait-popup__details--title">个人积分明细</div>
              <div class="portrait-popup__details--container">
                <div v-for="item in pointsDetails"
                     :key="item.id"
                     class="portrait-popup__details--item">
                  <div class="portrait-flex align-center">
                    <div class="portrait-flex-l">
                      <dl>
                        <dt>{{ item.name }}</dt>
                        <dd>{{ item.date }}</dd>
                      </dl>
                    </div>
                    <div class="portrait-flex-s">
                      <span>{{ item.points }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </el-collapse-item>
          </el-collapse>
        </div>
      </div>
      <div slot="reference"
           class="portrait-popup__reference portrait-flex align-center">
        <div class="portrait-flex-s">
          <div class="portrait-popup__avatar">
            <img :src="userInfo.avatar || userAvatarNone"
                 :style="{borderColor: badgeLevel.color}"
                 alt="avatar"
                 class="portrait-popup__avatar--main" />
            <div class="portrait-popup__subscript">
              <img :src="badgeLevel.icon"
                   alt="subscript" />
            </div>
          </div>
        </div>
        <!-- 如果需要/不需要名字可以显示/隐藏以下div: portrait-flex-l -->
        <!-- <div class="portrait-flex-l">
          <div class="portrait-popup__name">{{ userInfo.name }}</div>
        </div> -->
      </div>
    </el-popover>
  </div>
</template>

<script>
import './index.css'

export default {
  name: 'PortraitPopup',
  data () {
    return {
      visible: true,
      activeCollapse: [],
      userAvatarNone: require('./images/avatar-none.png'),
      badges: [
        {
          id: '1',
          name: '金鹭',
          minPoints: 2000,
          color: '#ffc757',
          icon: require('./images/badge-gold.png'),
          iconTie: require('./images/badge-gold-tie.png')
        },
        {
          id: '2',
          name: '银鹭',
          minPoints: 1000,
          color: '#d1d8d8',
          icon: require('./images/badge-silver.png'),
          iconTie: require('./images/badge-silver-tie.png')
        },
        {
          id: '3',
          name: '铜鹭',
          minPoints: 100,
          color: '#e6a258',
          icon: require('./images/badge-copper.png'),
          iconTie: require('./images/badge-copper-tie.png')
        },
        {
          id: '4',
          name: '白鹭',
          minPoints: 0,
          color: '#ffeee0',
          icon: require('./images/badge-white.png'),
          iconTie: require('./images/badge-white-tie.png')
        }
      ],
      userInfo: {
        name: '头像带名字',
        avatar: require('./images/avatar-none.png'),
        points: 1320
      },
      pointsDetails: [
        {
          id: '1',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '2',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '3',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '4',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '-20'
        },
        {
          id: '5',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '6',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '-300'
        },
        {
          id: '7',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '8',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '9',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        },
        {
          id: '10',
          name: '程序出版',
          date: '2020-08-23 12:23:52',
          points: '+10'
        }
      ]
    }
  },
  computed: {
    badgeLevel () {
      const { points = 0 } = this.userInfo
      for (let i = 0; i < this.badges.length; i++) {
        const { minPoints = 0 } = this.badges[i]
        if (points >= minPoints) {
          return this.badges[i]
        }
      }
      return {}
    },
    lastLevel () {
      const currentIndex = this.badges.findIndex(badge => badge.id === this.badgeLevel.id)
      const lastLevel = this.badges[currentIndex - 1]
      return lastLevel
    }
  },
  methods: {
    getProgress () {
      let progress = 0
      const maxLevel = this.badges[0]
      if (maxLevel && this.userInfo) {
        progress = this.userInfo.points / maxLevel.minPoints * 100
      }

      // 由于10%的比例过小，所以乘以2.5以作展示
      if (progress <= 10) {
        progress *= 2.5
      }

      return progress + '%'
    },
    getPosition (badge) {
      let positionLeft = 0
      const maxLevel = this.badges[0]
      if (maxLevel && badge) {
        positionLeft = badge.minPoints / maxLevel.minPoints * 100
      }

      // 由于10%的比例过小，所以乘以2.5以作展示
      if (positionLeft <= 10) {
        positionLeft *= 2.5
      }

      return positionLeft + '%'
    },
    isPositionActive (badge) {
      return this.userInfo.points >= badge.minPoints
    }
  }
}
</script>
