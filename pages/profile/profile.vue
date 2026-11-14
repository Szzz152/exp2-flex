<template>
  <view class="page">
    <!-- 头部资料区：纵向排列、交叉轴居中 -->
    <view class="header">
      <view class="avatar">
        <text class="avatar-text">{{ nickname.charAt(0) }}</text>
      </view>
      <text class="nickname">{{ nickname }}</text>
      <view class="tags">
        <text class="tag" v-for="t in tags" :key="t">{{ t }}</text>
      </view>
    </view>

    <!-- 数据概览：三个等宽列，用 flex:1 平分 -->
    <view class="stats">
      <view class="stat" v-for="s in stats" :key="s.label">
        <text class="stat-num">{{ s.value }}</text>
        <text class="stat-label">{{ s.label }}</text>
      </view>
    </view>

    <!-- 功能菜单卡片：每行横向，圆点-文字(占满)-箭头 -->
    <view class="menu">
      <view
        class="menu-item"
        v-for="(item, idx) in menus"
        :key="item.text"
        :class="{ noBorder: idx === menus.length - 1 }"
      >
        <text class="menu-dot"></text>
        <text class="menu-text">{{ item.text }}</text>
        <text class="menu-arrow">›</text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// 页面展示数据：用 ref 声明响应式状态，改数据界面自动更新
const nickname = ref<string>('开发者小王')
const tags = ref<string[]>(['UniApp 达人', '前端工程师'])

const stats = ref([
  { label: '学习时长', value: '128h' },
  { label: '完成实验', value: '7' },
  { label: '获得勋章', value: '12' }
])

interface MenuItem {
  text: string
}

const menus = ref<MenuItem[]>([
  { text: '我的课程' },
  { text: '学习进度' },
  { text: '成就勋章' },
  { text: '消息通知' },
  { text: '设置' }
])
</script>

<style>
.page {
  min-height: 100vh;
  background: #f2f4f8;
}

/* 头部：column 方向（默认），align-items 交叉轴居中 */
.header {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 80rpx 40rpx 56rpx;
  background: linear-gradient(135deg, #1F3A8C 0%, #07A35A 100%);
}

.avatar {
  width: 140rpx;
  height: 140rpx;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.22);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20rpx;
}

.avatar-text {
  font-size: 60rpx;
  color: #fff;
  font-weight: bold;
}

.nickname {
  font-size: 38rpx;
  color: #fff;
  font-weight: bold;
  margin-bottom: 18rpx;
}

.tags {
  display: flex;
  flex-direction: row;
}

.tag {
  font-size: 22rpx;
  color: #fff;
  background: rgba(255, 255, 255, 0.22);
  padding: 8rpx 24rpx;
  border-radius: 24rpx;
  margin: 0 8rpx;
}

/* 概览卡：向上偏移压住头部；三列 flex:1 等宽 */
.stats {
  display: flex;
  flex-direction: row;
  margin: -32rpx 24rpx 0;
  background: #fff;
  border-radius: 20rpx;
  box-shadow: 0 8rpx 24rpx rgba(31, 58, 140, 0.10);
}

.stat {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 28rpx 0;
}

.stat-num {
  font-size: 36rpx;
  font-weight: bold;
  color: #1F3A8C;
}

.stat-label {
  font-size: 24rpx;
  color: #8a909c;
  margin-top: 8rpx;
}

/* 菜单：每行 row，文字 flex:1 占满，箭头挤到最右 */
.menu {
  margin: 24rpx;
  background: #fff;
  border-radius: 20rpx;
  padding: 0 28rpx;
}

.menu-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 34rpx 0;
  border-bottom: 1rpx solid #eef0f4;
}

.menu-item.noBorder {
  border-bottom: none;
}

.menu-dot {
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  background: #1F3A8C;
  margin-right: 22rpx;
}

.menu-text {
  flex: 1;
  font-size: 30rpx;
  color: #222a35;
}

.menu-arrow {
  font-size: 36rpx;
  color: #c0c4cc;
}
</style>
