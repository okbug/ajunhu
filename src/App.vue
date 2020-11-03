<template>
  <div class="container">
    <h1>Hello</h1>
    <GlobalHeader :user="currentUser" />
    <ValidateInput :rules="emailRules"/>
    <ColumnList :list="list" />

  </div>
</template>

<script lang="ts">
import 'bootstrap/dist/css/bootstrap.min.css'
import { defineComponent, reactive } from 'vue'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'id=1的专栏',
    description: 'This is just a test desc1',
    avatar: require('@/assets/avatar.jpg')
  },
  {
    id: 2,
    title: 'id=2的专栏',
    description: 'This is just a test desc2',
    avatar: require('@/assets/avatar.jpg')
  },
  {
    id: 3,
    title: 'id=3的专栏',
    description: 'This is just a test desc3',
    avatar: require('@/assets/avatar.jpg')
  },
  {
    id: 4,
    title: 'id=4的专栏',
    description: 'This is just a test desc4'
  }
]
const currentUser: UserProps = {
  isLogin: true,
  name: '阿君哥',
  id: 1
}
export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    ValidateInput
  },
  setup () {
    const emailRules: RulesProp = [
      { type: 'required', message: '不能为空' },
      { type: 'email', message: '输入错误' }
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    return {
      list: testData,
      currentUser,
      emailRules,
      emailRef
    }
  }
})
</script>

<style>

</style>
