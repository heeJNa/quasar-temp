<template>
  <q-dialog v-model="inception" :persistent="true">
    <q-card class="work-unit-upload">
      <q-card-section style="display: flex; justify-content: space-between;">
        <div class="text-h5" style="display: inline-block;">작업 단위 등록</div>
        <q-btn no-caps label="X" color="primary" @click="this.$emit('close')"/>
      </q-card-section>
      <q-card-section class="q-pt-none">
        <div class="row ">
          <div class="col-sm-6">
            <div class="column basic-info">
              <div class="col-md-3 text-h6 q-pl-lg">
                기본정보
              </div>
              <q-separator spaced="lg" />
              <div class="col-md-3 row inline justify-around">
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
              </div>
              <q-separator spaced="lg" color="white"/>
              <div class="col-md-3 row inline justify-around">
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
              </div>
              <q-separator spaced="lg" color="white"/>
              <div class="col-md-3 row inline justify-around">
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" />
              </div>
            </div>
          </div>
          <div class="col-sm-6">
            <div class="column basic-info">
              <div class="col-md-3 text-h6 q-pl-lg row">
                작업 파일 리스트
                <q-select v-model="searchForm.company" outlined dense :options="companies" label="보험사" class="q-ml-lg" />
              </div>
              <q-separator spaced="lg" />
            </div>
          </div>
        </div>
        <q-separator spaced="lg" color="white"/>
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
    const searchForm = reactive({
      company: '',
      lock:false,
      schedule: '',
    })
    const onFileUnitUpload = () => {
      emit('close')
    }
    return {
      searchForm,
      onFileUnitUpload
    }
  },
}
</script>

<style scoped>
.work-unit-upload {
  max-width: 1200px;
  width: 1200px;
  height: 450px;
}
.col-sm-12 .q-select{
  width: 48%;
}
.file-unit-upload .row div:not(:nth-last-child(1)){
  margin-bottom: 20px;
}
.file-unit-upload .q-input,.q-select {
  width: 96%;
}
.basic-info .q-select{
  width:240px;
}
</style>
