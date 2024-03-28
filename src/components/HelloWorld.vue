<template>
  <div class="hello">
    <div class="header">
      <div class="title">个人信息</div>
      <div class="btn" @click="onClick">{{ editState ? '保存' : '编辑' }}</div>
    </div>
    <div class="divider">基本信息</div>
    <component :is="componentId" :userInfo="userInfo" ref="myCompoent"></component>
  </div>
</template>
<script>
import PreviewView from './PreviewView.vue';
import ZdyForm from './ZdyForm.vue';
import _ from 'lodash';
export default {
  name: 'HelloWorld',
  components: {
    PreviewView,
    ZdyForm,
  },
  data() {
    return {
      userInfo: [
        {
          label: '姓名',
          value: '',
          required: true,
          type: 'input',
          name: 'name',
        },
        {
          label: '出生日期',
          value: '',
          required: true,
          type: 'datePicker',
          name: 'brithDate',
        },
        {
          label: '政治面貌',
          value: '',
          required: true,
          type: 'select',
          columns: ['群众', '共青团员', '共产党员'],
          name: 'political',
        },
        {
          label: '性别',
          value: '',
          required: true,
          type: 'select',
          columns: ['男', '女'],
          name: 'sex',
        },
        {
          label: '手机号',
          value: '',
          required: true,
          type: 'input',
          name: 'phone',
          regex: /^1([358][0-9]|4[579]|66|7[0135678]|9[89])[0-9]{8}$/, // eslint-disable-line
        },
        {
          label: '邮箱',
          value: '',
          required: true,
          type: 'input',
          name: 'email',
          regex: /^[A-Za-z0-9_\-\.]+\@[A-Za-z0-9_\-\.]+\.([A-Za-z]{2,4})$/, // eslint-disable-line
        },
        {
          label: '身份证件号',
          value: '',
          required: true,
          type: 'input',
          name: 'idenit',
          regex: /^[1-9]\d{5}(19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9X]$/, // eslint-disable-line
        },
        {
          label: '所在单位',
          value: '',
          required: true,
          type: 'input',
          name: 'company',
        },
        {
          label: '所在岗位',
          value: '',
          required: true,
          type: 'input',
          name: 'job',
        },
      ],
      editState: false,
    };
  },
  computed: {
    componentId() {
      return this.editState ? ZdyForm : PreviewView;
    },
  },
  created() {
    let userInfo = localStorage.getItem('blocklet_userInfo');
    try {
      userInfo = JSON.parse(userInfo);
    } catch (error) {
      userInfo = null;
    }
    if (userInfo) {
      for (const key in userInfo) {
        if (userInfo[key]) {
          const index = _.findIndex(this.userInfo, { name: key });
          this.userInfo[index].value = userInfo[key];
        }
      }
    }
  },
  methods: {
    validForm() {
      return new Promise((resolve, reject) => {
        let res = {};
        this.userInfo.forEach((item) => {
          if (item.required && item.value === '') {
            reject(`${item.label}不能为空`);
            throw new Error(`${item.label}不能为空`);
          }
          if (item.regex && item.value && !item.regex.test(item.value)) {
            reject(`请检查${item.label}格式`);
            throw new Error(`请检查${item.label}格式`);
          }
          res[item.name] = item.value;
        });
        resolve(res);
      });
    },
    async onClick() {
      if (this.editState) {
        try {
          const res = await this.validForm();
          localStorage.setItem('blocklet_userInfo', JSON.stringify(res));
          this.$toast('保存成功');
        } catch (error) {
          this.$toast(error);
          return;
        }
      }
      this.editState = !this.editState;
    },
  },
};
</script>
<style scoped lang="less">
.header {
  padding: 0.44rem 0.56rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  .title {
    color: #1a1d27;
    font-size: 0.4rem;
    font-weight: 600;
    line-height: 0.4rem;
  }
  .btn {
    background: linear-gradient(270deg, #5ed19e 0%, #07b7ae 100%);
    box-shadow: 0px 2px 8px 0rpx rgba(84, 206, 159, 0.5);
    border-radius: 0.32rem;
    width: 1.6rem;
    height: 0.64rem;
    line-height: 0.64rem;
    color: #fff;
    font-size: 0.24rem;
    text-align: center;
  }
}
.divider {
  width: 100%;
  height: 0.72rem;
  padding-left: 0.56rem;
  line-height: 0.72rem;
  color: #1a1d27;
  font-size: 0.28rem;
  background-color: #f6f6f6;
}
</style>
