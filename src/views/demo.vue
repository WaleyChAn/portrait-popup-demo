<template>
  <div class="demo-container">
    <div class="demo-header">
      <portrait-popup></portrait-popup>
      <span>某某某</span>
      <span>其他按钮</span>
    </div>
    <div class="demo-main"></div>
  </div>
</template>

<script>
import PortraitPopup from '@/components/portrait-popup/index.vue'

export default {
  name: 'Demo',
  components: {
    PortraitPopup
  }
}
</script>

<style>
.demo-container {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
  font-size: 14px;
  padding: 5px;
  box-sizing: border-box;
}

.demo-header {
  display: flex;
  justify-content: end;
  align-items: center;
  margin: 5px;
  height: 60px;
  box-sizing: border-box;
  background: #eee;
}

.demo-header > * {
  margin: 0 10px;
}

.demo-main {
  flex: 1;
  margin: 5px;
  box-sizing: border-box;
  background: #eee;
}
</style>
