<template>
  <div class="org-register">
    <el-header>
      <div class="logo">Logo</div>
      <el-menu mode="horizontal">
        <el-menu-item>排行榜</el-menu-item>
        <el-menu-item>待定</el-menu-item>
        <el-menu-item>待定</el-menu-item>
      </el-menu>
      <el-button-group>
        <el-button type="primary" plain>组织注册</el-button>
        <el-button type="primary">成员注册</el-button>
      </el-button-group>
    </el-header>

    <el-main>
      <!-- <el-form ref="form" :model="form" label-width="120px" @submit.prevent="submitForm"> -->
      <el-form ref="form" :model="form" label-width="120px">
        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="组织名称">
              <el-input v-model="form.name" placeholder="名称"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="组织介绍">
              <el-input
                v-model="form.link"
                placeholder="链接"
              ></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="联系邮箱">
              <el-input v-model="form.contactEmail" placeholder="邮箱"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="项目范围">
              <el-select v-model="form.category1" placeholder="请选择">
                <el-option
                  label="国家重点发展项目"
                  value="国家重点发展项目"
                ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="平台权限">
              <el-select v-model="form.category2" placeholder="请选择">
                <el-option
                  label="全球化模式：1:1:1"
                  value="全球化模式：1:1:1"
                ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="评价模型">
              <el-select v-model="form.category3" placeholder="请选择">
                <el-option
                  label="工信部标准院标准：网络模型"
                  value="工信部标准院标准：网络模型"
                ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="数据时间范围">
              <el-date-picker
                v-model="form.startDate"
                type="month"
                placeholder="XX年XX月"
              ></el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item>
              <el-date-picker
                v-model="form.endDate"
                type="month"
                placeholder="XX年XX月"
              ></el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="分析报告">
              <el-select v-model="form.category4" placeholder="请选择">
                <el-option label="普通版" value="普通版"></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="24" class="button-group">
            <el-button type="primary" plain>返回</el-button>
            <!-- <el-button type="primary" native-type="submit">完成注册</el-button> -->
            <el-button type="primary" v-on:click="submitForm">完成注册</el-button>
          </el-col>
        </el-row>
      </el-form>
    </el-main>

    <el-footer>
      <div class="footer-content">
        <img
          src="/images/lab-logo.png"
          alt="Xlab Logo"
          class="footer-logo"
        />
        <p>官方支持</p>
        <p>Copyright © 2024 X-lab</p>
      </div>
    </el-footer>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      form: {
        name: "",
        link: "",
        contactEmail: "",
        category1: "",
        category2: "",
        category3: "",
        startDate: "",
        endDate: "",
        category4: "",
      },
    };
  },
  methods: {
    submitForm() {
      // axios.post('/api/org/register', this.form)
      // this.$http.post('http://localhost:8081/org/register', this.form)
      this.$http.post("/org/register",this.form)
        .then(response => {
          console.log('注册成功', response.data);
          // 可添加成功提示或执行其他操作
          this.$message.success('注册成功！');
        })
        .catch(error => {
          console.error('注册失败', error);
          // 可添加错误提示或执行其他操作
          this.$message.error('注册失败：' + error.message);
        });
    },
  },
};
</script>

<style scoped>
.org-register {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.el-header {
  background: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.logo {
  font-size: 24px;
  font-weight: bold;
}

.el-menu {
  flex: 1;
  margin-left: 20px;
}

.el-main {
  flex: 1;
  padding: 50px;
  /* background: #f0f2f5; */
}

.el-footer {
  text-align: center;
  padding: 30px 0;
  background: #fff;
  border-top: 1px solid #eaeaea;
}

.footer-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.footer-logo {
  width: 50px;
  height: 50px;
  margin-bottom: 10px;
}

.button-group {
  text-align: center;
  margin-top: 20px;
}

.el-button:first-child {
  margin-left: 0;
}

.el-button--primary {
  color: #fff;
  background-color: #131313;
  border-color: #cdcdcd;
}

.el-button--primary:focus,
.el-button--primary:hover {
  background: #e8e8e8;
  border-color: #131313;
  color: #131313;
}

.el-button--primary.is-plain {
  color: #5f5f5f;
  background: #fff;
  border-color: #cdcdcd;
}

.el-button--primary.is-plain:focus,
.el-button--primary.is-plain:hover {
  background: #131313;
  border-color: #131313;
  color: #fff;
}
</style>