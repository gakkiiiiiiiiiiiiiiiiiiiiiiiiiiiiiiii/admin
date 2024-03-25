<template>
  <PageWrapper>
    <template #headerContent>
      <div
        ><a-button type="primary" @click="genImage"> 获取图像 </a-button>
        <a-button class="ml-2" @click="checkDot"> 检测墨点 </a-button>
      </div>
      <p v-if="isChecked">墨点数量：{{ num }}个</p>
    </template>
    <div class="lg:flex">
      <div class="lg:w-6/10 w-full enter-y">
        <Card class="!my-4 enter-y h-full">
          <IntDot :num="num" :checked="isChecked" />
        </Card>
      </div>
      <div class="lg:w-4/10 w-full enter-y pl-4">
        <Card class="!my-4 enter-y h-full">
          <Form>
            <FormItem label="墨滴">
              <div class="w-100px"><input-number /></div>
            </FormItem>
            <FormItem label="亮度">
              <div class="w-100px"><input-number /></div>
            </FormItem>
          </Form>

          <Table
            bordered
            :dataSource="tableData"
            :columns="[
              { title: 'No', dataIndex: 'no', key: 'no' },
              { title: 'Vel(m/s)', dataIndex: 'vel', key: 'vel' },
              { title: 'Voll(PL)', dataIndex: 'voll', key: 'voll' },
            ]"
          />
        </Card>
      </div>

      <!-- <div class="lg:w-7/10 w-full !mr-4 enter-y">
        <ProjectCard :loading="loading" class="enter-y" />
        <DynamicInfo :loading="loading" class="!my-4 enter-y" />
      </div>
      <div class="lg:w-3/10 w-full enter-y">
        <QuickNav :loading="loading" class="enter-y" />

        <Card class="!my-4 enter-y" :loading="loading">
          <img class="xl:h-50 h-30 mx-auto" src="../../../assets/svg/illustration.svg" />
        </Card>

        <SaleRadar :loading="loading" class="enter-y" />
      </div> -->
    </div>
  </PageWrapper>
</template>
<script lang="ts" setup>
  import { ref } from 'vue'
  import { Card, Form, FormItem, InputNumber, Table } from 'ant-design-vue'
  import { PageWrapper } from '/@/components/Page'

  import IntDot from './components/IntDot.vue'
  import { message } from 'ant-design-vue'
  const loading = ref(false)

  const num = ref(0)
  const isChecked = ref(false)
  function getRandomNumber() {
    return Math.floor(Math.random() * 20) + 1
  }
  const genImage = () => {
    num.value = 0
    isChecked.value = false
    loading.value = true
    setTimeout(() => {
      num.value = getRandomNumber()
      loading.value = false
    }, 1000)
  }

  const checkDot = () => {
    loading.value = true
    setTimeout(() => {
      loading.value = false
      isChecked.value = true
      message.info(`墨点检测完成，检测到墨点数量${num.value}个`)
    }, 2000)
  }

  const tableData = Array.from({ length: 10 }).map((_, i) => {
    return {
      no: i + 1,
      vel: `5.${i + 1}`,
      voll: `10.${i + 1}`,
    }
  })
</script>
