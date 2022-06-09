<template>
  <q-dialog v-model="inception" :persistent="true" @before-show="init">
    <q-card class="work-unit-upload">
      <q-card-section style="display: flex; justify-content: space-between">
        <div class="text-h5" style="display: inline-block">작업 단위 등록</div>
        <q-btn no-caps label="X" color="primary" @click="this.$emit('close')" />
      </q-card-section>
      <q-card-section class="q-pt-none">
        <div class="row">
          <div class="col-sm-6">
            <div class="column basic-info">
              <div class="col-md-3 text-h6 q-pl-lg">기본정보</div>
              <q-separator spaced="lg" color="grey-3"/>
              <div class="col-md-3 row inline justify-around">
                <q-select
                  v-model="uploadForm.company"
                  outlined
                  dense
                  :options="companies"
                  label="회사명"
                />
                <q-select
                  v-model="uploadForm.insurance"
                  outlined
                  dense
                  :options="companies"
                  label="보험사"
                />
              </div>
              <q-separator spaced="lg" color="white" />
              <div class="col-md-3 row inline justify-around">
                <q-select
                  v-model="uploadForm.id"
                  outlined
                  dense
                  :options="companies"
                  label="계정명"
                />
                <q-input
                  v-model="uploadForm.schedule"
                  style="width: 240px;"
                  outlined=""
                  dense
                  label="일정"
                />
              </div>
              <q-separator spaced="lg" color="white" />
              <div class="col-md-3 row" style="margin-left:26px">
                <q-select
                  v-model="uploadForm.ERPConnect"
                  outlined
                  dense
                  :options="companies"
                  label="ERP연동"
                />
              </div>
            </div>
          </div>
          <q-separator vertical spaced="lg" color="white"/>
          <div class="col-sm-5">
            <div class="column basic-info">
              <div class="col-md-3 text-h6 q-pl-lg row">
                작업 파일 리스트
                <q-select
                  v-model="uploadForm.company"
                  outlined
                  dense
                  :options="companies"
                  label="보험사"
                  class="q-ml-lg"
                />
              </div>
              <q-separator spaced="lg" />
              <q-table :rows="data" :columns="columns" row-key="fileName" :hide-bottom="true" class="work-table">
                <template v-slot:body-cell-timeout="props">
                  <q-td :props="props">
                    <q-input :props="props" v-model="props.row.timeout"/>
                  </q-td>
                </template>
                <template v-slot:body-cell-생성여부="props">
                  <q-td :props="props">
                    <q-checkbox :props="props" v-model="props.row.create"/>
                  </q-td>
                </template>
              </q-table>
            </div>
          </div>
        </div>
        <q-separator spaced="lg" color="white" />
        <div class="text-center">
          <q-btn color="primary" label="등록" @click="onFileUnitUpload" />
        </div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>
<script>
import { reactive } from "vue";

const columns = [
  { name: "파일명", label: "파일명", field: "fileName", align: "center" },
  {
    name: "보종",
    label: "보종",
    field: "spec",
    align: "center",
    sortable: true,
  },
  { name: "콘텐츠", label: "콘텐츠", field: "content", align: "center" },
  { name: "timeout", label: "Timeout(ms)", field: "timeout", align: "center" },
  {
    name: "생성여부",
    label: "생성여부",
    field: "create",
    align: "center",
  },
];
const data = reactive([
  {
    fileName: "first file",
    spec: '신계약',
    content: "에즈금융서비스",
    timeout: 123456789,
    create: true,
  },])
export default {
  props: ["inception", "companies"],
  emit: ["close"],

  setup(props, { emit }) {
    const uploadForm = reactive({
      company: "",
      insurance: "",
      schedule: "",
      id:"",
      ERPConnect:"",
    });
    // 공통함수로 만들기
    const init = () => {
      uploadForm.company= "",
      uploadForm.insurance = "",
      uploadForm.schedule = "",
      uploadForm.id = "",
      uploadForm.ERPConnect = ""
    }
    const onFileUnitUpload = () => {
      emit("close");
    };
    return {
      init,
      onFileUnitUpload,
      uploadForm,
      data,
      columns
    };
  },
};
</script>

<style scoped>
.work-unit-upload {
  max-width: 1200px;
  width: 1200px;
  height: 450px;
}
.col-sm-12 .q-select {
  width: 48%;
}
.file-unit-upload .row div:not(:nth-last-child(1)) {
  margin-bottom: 20px;
}
.file-unit-upload .q-input,
.q-select {
  width: 96%;
}
.basic-info .q-select {
  width: 240px;
}
</style>
