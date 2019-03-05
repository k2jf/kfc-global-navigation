<template>
  <Header>
    <div class="logo-wrapper">
      <img src="../assets/header_logo.png" />
    </div>
    <div class="right-wrapper">
      <slot name="right-header">
        <Button>退出</Button>
      </slot>
    </div>
  </Header>
</template>
<script>
import { Header, Button } from 'iview'
export default {
  name: 'GlobalHeader',
  components: {
    Header,
    Button
  }
}
</script>

<style scoped lang="css">
.logo-wrapper {
  height: 100%;
  padding: 12px 0;
  float: left;
}
.right-wrapper {
  height: 100%;
  float: right;
}
</style>
