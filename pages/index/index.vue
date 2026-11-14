<template>
  <view class="page">

    <!-- ① 顶部用户区：横向容器，主轴两端对齐、交叉轴居中 -->
    <view class="card header">
      <image class="avatar" src="/static/avatar.png" mode="aspectFill"></image>
      <view class="info">
        <text class="name">{{ user.name }}</text>
        <text class="desc">{{ user.desc }}</text>
      </view>
      <button class="edit-btn" size="mini">编辑</button>
    </view>

    <!-- ② 数据统计：横向容器，三个子项用 flex:1 等分权重 -->
    <view class="card stats">
      <view class="stat" v-for="(item, index) in stats" :key="index">
        <text class="num">{{ item.num }}</text>
        <text class="label">{{ item.label }}</text>
      </view>
    </view>

    <!-- ③ 功能列表：纵向容器，每行横向两端对齐 -->
    <view class="card list">
      <view class="row" v-for="(item, index) in menus" :key="index">
        <text class="row-title">{{ item }}</text>
        <text class="row-arrow">›</text>
      </view>
    </view>

    <!-- ④ 底部操作区：横向容器，交叉轴居中 -->
    <view class="footer">
      <button class="primary-btn" type="primary">开始学习</button>
    </view>

  </view>
</template>

<script setup>
import { ref } from 'vue'

const user = ref({
  name: '张三',
  desc: 'Web 前端开发 · 大二'
})

const stats = ref([
  { num: 12, label: '课程' },
  { num: 86, label: '作业' },
  { num: 3, label: '待办' }
])

const menus = ref(['我的课程', '作业记录', '设置'])
</script>

<style>
/* ============================================================
   根容器：纵向弹性布局（主轴 = 垂直方向）
   ============================================================ */
.page {
  display: flex;
  flex-direction: column;          /* 主轴：垂直，子元素自上而下排列 */
  min-height: 100vh;
  padding: 32rpx;
  box-sizing: border-box;
  background-color: #F5F6FA;
}

/* 通用卡片：白色底 + 圆角 + 间距 */
.card {
  background-color: #FFFFFF;
  border-radius: 24rpx;
  padding: 32rpx;
  margin-bottom: 24rpx;
}

/* ============================================================
   ① 顶部用户区
   主轴水平：justify-content 控制左右怎么分
   交叉轴垂直：align-items 控制上下怎么对
   ============================================================ */
.header {
  display: flex;
  flex-direction: row;            /* 主轴：水平，子元素从左到右 */
  justify-content: space-between; /* 主轴：两端对齐，中间留白 */
  align-items: center;            /* 交叉轴：垂直居中 */
}

.avatar {
  width: 120rpx;                  /* rpx：屏幕适配单位 */
  height: 120rpx;
  border-radius: 60rpx;
  flex-shrink: 0;
}

/* 权重分配：占满头像与按钮之间的剩余宽度 */
.info {
  flex: 1;
  display: flex;
  flex-direction: column;
  margin-left: 24rpx;
}

.name {
  font-size: 36rpx;
  font-weight: bold;
  color: #1F2233;
}

.desc {
  font-size: 26rpx;
  color: #8A8F9C;
  margin-top: 8rpx;
}

.edit-btn {
  margin: 0 0 0 16rpx;
  font-size: 24rpx;
  color: #4B6BFB;
  background-color: #EEF1FF;
  border-radius: 24rpx;
}

/* ============================================================
   ② 数据统计：横向容器 + 三项等分
   ============================================================ */
.stats {
  display: flex;
  flex-direction: row;
}

/* 权重分配：三个子项各占 1 份，自动等分整行宽度 */
.stat {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.num {
  font-size: 44rpx;
  font-weight: bold;
  color: #1F2233;
}

.label {
  font-size: 24rpx;
  color: #8A8F9C;
  margin-top: 8rpx;
}

/* ============================================================
   ③ 功能列表：纵向容器 + 每行两端对齐
   ============================================================ */
.list {
  padding-top: 0;
  padding-bottom: 0;
}

.row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;  /* 主轴：标题靠左、箭头靠右 */
  align-items: center;
  padding: 32rpx 0;
  border-bottom: 1rpx solid #F0F1F5;
}

.row:last-child {
  border-bottom: none;
}

.row-title {
  font-size: 30rpx;
  color: #1F2233;
}

.row-arrow {
  font-size: 34rpx;
  color: #C5C9D4;
}

/* ============================================================
   ④ 底部操作区：交叉轴居中，按钮按权重伸展
   ============================================================ */
.footer {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: auto;                /* 推到页面最底部 */
  padding-top: 24rpx;
}

.primary-btn {
  flex: 1;
  height: 88rpx;
  line-height: 88rpx;
  font-size: 32rpx;
  border-radius: 44rpx;
  background-color: #4B6BFB;
  color: #FFFFFF;
}
</style>
