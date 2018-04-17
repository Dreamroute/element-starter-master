<template>
  <div>
    <el-tabs type="border-card" closable="true">
      <el-tab-pane v-for="tab in tabs" :label="tab.label">{{tab.label}}</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
    export default {
        name: "",
        data() {
            return {
                tabs: [
                    {label: '用户管理'},
                    {label: '配置管理'},
                    {label: '角色管理'},
                ]
            }
        }
    }
</script>

<style scoped>

</style>