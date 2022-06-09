<template>
  <q-dialog v-model="inception" :persistent="true">
    <q-card class="work-unit-upload">
      <q-card-section style="display: flex; justify-content: space-between" class="q-pb-none">
        <div class="text-h5" style="display: inline-block">기본정보</div>
        <q-btn no-caps label="X" color="primary" @click="this.$emit('close')" />
      </q-card-section>
      <q-card-section class="q-pa-lg">
        <div class="row">
          <div class="col-6 q-pa-md">
            <q-input
              dense
              v-model="editForm.company_name"
              outlined
              disable
              label="회사명"
            />
          </div>
        </div>
        <div class="row">
          <div class="col q-pa-md">
            <q-input
              dense
              v-model="editForm.insure_name"
              outlined
              disable
              label="보험사"
            />
          </div>
          <div class="col q-pa-md">
            <q-input
              dense
              v-model="editForm.계정"
              outlined
              disable
              label="계정명"
            />
          </div>
        </div>
        <div class="row">
          <div class="col q-pa-md">
            <q-input
              dense
              v-model="editForm.work_kind"
              outlined
              disable
              label="작업"
            />
          </div>
          <div class="col q-pa-md">
            <q-input
              dense
              v-model="editForm.filename"
              outlined
              disable
              label="파일명"
            />
          </div>
        </div>
        <div class="row">
          <div class="col q-pa-md">

            <q-input dense v-model="editForm.schedule" outlined label="일정" />
          </div>
          <div class="col q-pa-md">
            <q-input
              dense
              v-model="editForm.timeout"
              outlined
              label="Timeout(ms)"
            />
          </div>
        </div>
        <div class="row">
          <div class="col q-pa-md">
            <q-select outlined dense :options="options" label="ERP연동"/>
          </div>
          <div class="col q-pa-md">
            <q-checkbox v-model="editForm.lock" :label-slot="true" label="잠금" left-label>
              <template v-slot:label>
                  잠금
              </template>
            </q-checkbox>
          </div>
        </div>
        <q-separator spaced="10px" color="white"/>
        <div class="text-center flex justify-center">
          <div>
            <q-btn color="amber" label="수정" @click="onFileUnitUpload" />
          </div>
          <div class="q-pl-md">
            <q-btn color="red" label="삭제" @click="onFileUnitUpload" />
          </div>
        </div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>
<script>
import { computed, reactive } from "vue";

export default {
  props: ["inception", "workDetail"],
  emit: ["close"],

  setup(props, { emit }) {
    const editForm = computed(()=>props.workDetail);
    const onFileUnitUpload = () => {
      console.log(editForm)
      emit("close");
    };
    const options = [
      '지넥슨ERP'
    ]
    return {
      options,
      onFileUnitUpload,
      editForm,
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
