<template>
  <q-dialog v-model="inception" :persistent="true" @before-show="init">
    <q-card class="file-unit-upload">
      <q-card-section style="display: flex; justify-content: space-between;">
        <div class="text-h6" style="display: inline-block;">파일 단위 작업 등록</div>
        <q-btn no-caps label="X" color="primary" @click="this.$emit('close')"/>
      </q-card-section>
      <q-card-section class="q-pt-none">
        <div class="row">
          <div class="col-6 q-mb-md">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="회사명" />
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="보험사" />
          </div>
          <div class="col-6">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="계정명" />
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="작업" />
          </div>
          <div class="col-6">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="파일명" />
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <q-input outlined type="text" label="일정" dense  v-model="createForm.schedule"/>
          </div>
          <div class="col-6">
            <q-input outlined type="text" label="Timeout(ms)" dense />
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <q-select v-model="createForm.company" outlined dense :options="companies" label="ERP연동" />
          </div>
          <div class="col-6">
            <q-checkbox v-model="createForm.lock" label="잠금" />
          </div>
        </div>
          <div class="text-center">
            <q-btn color="primary" label="등록" @click="onFileUnitUpload"/>
          </div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>
<script>
import { reactive } from 'vue'

export default {
  props: ['inception','companies'],
  emit: ['close'],
  setup(props,{emit}) {
    const createForm = reactive({
      company: '',
      lock:false,
      schedule: '',
    })
    const onFileUnitUpload = () => {
      emit('close')
    }
    const init = () => {
      createForm.company = ''
      createForm.lock = false
      createForm.schedule = ''
    }
    return {
      createForm,
      init,
      onFileUnitUpload
    }
  },
}
</script>

<style scoped>
.file-unit-upload {
  width: 600px;
  height: 424px;
}
.file-unit-upload .row div:not(:nth-last-child(1)){
  margin-bottom: 20px;
}
.file-unit-upload .q-input,.q-select {
  width: 96%;
}
</style>
