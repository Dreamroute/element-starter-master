<template>
  <div>
    <el-container>
      <el-header style="height: 70px; padding: 0">
      </el-header>
      <el-container>
        <el-aside width="200px">
          <div>
            <el-menu @open="handleOpen" @close="handleClose">
              <el-submenu index="1">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>系统管理</span>
                </template>
                <el-menu-item-group>
                  <el-menu-item index="1-1" @click="addTab">会员管理</el-menu-item>
                  <el-menu-item index="1-2">字典管理</el-menu-item>
                </el-menu-item-group>
              </el-submenu>
              <el-submenu index="2">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>基础管理</span>
                </template>
                <el-menu-item-group>
                  <el-menu-item index="2-1">开发者管理</el-menu-item>
                  <el-menu-item index="2-2">订单管理</el-menu-item>
                </el-menu-item-group>
              </el-submenu>
            </el-menu>
          </div>
        </el-aside>
        <el-main style="padding: 0px;">
          <div>
            <el-tabs type="border-card" :addable="true" :closable="true" v-model="selected">
              <el-tab-pane v-for="tab in tabs" :label="tab.label" :key="tab.label" :name="tab.label">
                <component :is="tab.contents"></component>
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-main>
      </el-container>
    </el-container>
    <el-dialog title="错误提示" :visible.sync="dialogVisible" width="20%" :before-close="handleClose">
      <span>您打开的标签过多，请关闭其他</span>
      <span slot="footer" class="dialog-footer">
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
    </el-dialog>
  </div>
</template>

<script>
    import West from './West'

    export default {
        name: "",
        components: {
            West
        },
        data() {
            return {
                tabs: [
                    {label: '用户管理', contents: West},
                    {label: '配置管理', contents: West},
                    {label: '角色管理', contents: West},
                ],
                selected: '用户管理',
                dialogVisible: false
            }
        },
        methods: {
            handleOpen(key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose(key, keyPath) {
                console.log(key, keyPath);
            },
            addTab(comp) {
                console.log(comp)
                if (this.tabs.length >= 10) {
                    this.dialogVisible = true;
                    return;
                }
                let tab = {label: '权限管理', contents: West};
                let exists = false;
                this.tabs.forEach(t => {
                    if (t.label === tab.label) {
                        exists = true;
                    }
                })
                if (!exists) {
                    this.tabs.push(tab);
                }
                this.selected = tab.label;
            }
        }
    }
</script>

<style scoped>
  .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    height: 80px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    height: 850px;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
  }

  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }

  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
</style>