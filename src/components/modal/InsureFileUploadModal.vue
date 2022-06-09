<template>
  <q-dialog :model-value="inception" :persistent="true" @before-show="init">
    <q-card class="work-unit-upload">
      <q-card-section style="display: flex; justify-content: space-between" class="q-pb-none">
        <div class="text-h5" style="display: inline-block">보험사 파일</div>
        <q-btn no-caps label="X" color="primary" @click="this.$emit('close')" />
      </q-card-section>
      <q-card-section class="q-pa-lg">
        <div class="row">
          <div class="col q-pa-md">
            <q-select v-model="createForm.file_code" outlined dense :options="gaList" label="GA" />
          </div>
          <div class="col q-pa-md">
            <q-select v-model="createForm.file_code" outlined dense :options="gaList" label="파일코드" />
          </div>
        </div>
        <div class="row">
          <div class="col q-pa-md">
            <q-select v-model="createForm.file_code" outlined dense :options="gaList" label="보험사" />
          </div>
          <div class="col q-pa-md">
            <q-input v-model="createForm.insurance" outlined dense label="메모" />
          </div>
        </div>
        <div class="row">
          <div class="col-6 q-pa-md">
            <q-file color="purple-12" v-model="createForm.insurance" label="첨부파일">
              <template v-slot:prepend>
                <q-icon name="attach_file" />
              </template>
            </q-file>
          </div>
        </div>
        <q-separator spaced="10px" color="white"/>
        <div class="text-center flex justify-center">
          <div>
            <q-btn color="primary" label="등록" @click="onFileUnitUpload" />
          </div>
        </div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>
<script>
import { computed, reactive } from "vue";

export default {
  props: ["inception"],
  emit: ["close"],

  setup(props, { emit }) {
    const createForm = reactive({
      ga:'',
      file_code:'',
      insurance:''
    })
    const onFileUnitUpload = () => {
      emit("close");
    };
    const init = () => {
      createForm.file_code = ''
      createForm.ga = ''
      createForm.insurance = ''
    }
    const options = [
      '지넥슨ERP'
    ]
    return {
      options,
      init,
      onFileUnitUpload,
      gaList:['인카','유어즈에셋','마이금융파트너']
      ,createForm
    };
  },
};
</script>

<style scoped>
.work-unit-upload {
  max-width: 800px;
  width: 800px
}
.col-sm-12 .q-select {
  width: 48%;
}
.file-unit-upload .row div:not(:nth-last-child(1)) {
  margin-bottom: 20px;
}

</style>
