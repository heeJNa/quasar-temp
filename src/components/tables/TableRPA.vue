<template>
  <q-card>
    <q-card-section class="q-pa-none">
      <q-table :rows="data" :columns="columns" row-key="no" :filter="filter" selection="multiple"
        v-model:selected="selected" v-model:pagination="pagination" no-data-label="데이터가 없습니다."
        no-results-label="결과가 없습니다." separator="cell">
        <template v-slot:body-cell-Create="props">
          <q-td :props="props">
            <q-btn color="primary" label="작업생성"/>
          </q-td>
        </template>
        <template v-slot:top>
          <q-select v-model="searchForm.company" outlined dense :options="companies" label="회사명" />
          <q-select v-model="searchForm.spec" outlined dense :options="spec" label="구분" />
          <q-select v-model="searchForm.insure" outlined dense :options="insure" label="보험사" />
          <q-select v-model="searchForm.work" outlined dense :options="wokr_kind" label="작업" />
          <q-select v-model="searchForm.lock" outlined dense :options="lockCheck" label="잠김 여부" />
          <q-btn color="brown-5" label="검색" />
          <q-space style="flex-basis: 100%;" />
          <div class="work-info" style="display: flex; ">
            <span class="q-px-sm work-total" style="padding-top: 13px;">total: 1,110건</span>
            <q-separator inset="true" />
            <div class="work-pagination q-pt-sm">
              <q-pagination v-model="pagination.page" :max="5" direction-links boundary-links />
            </div>
            <q-separator inset="true" />
            <div style="display: flex;" class="work-rowNum">
              <span style="padding-top: 13px;">개수:</span>
              <q-select v-model="pagination.rowsNumber" :options="[20, 40, 60, 80, 100]" dense />
            </div>
          </div>
          <q-space />
          <div>
            <q-btn color="primary" label="파일 단위 등록" @click="fileModal = true" style="margin-right: 15px" />
            <q-btn color="primary" label="작업 단위 등록" @click="workModal = true" />
          </div>
        </template>
        <template v-slot:no-data="{ icon, message, filter }">
          <div class="full-width row flex-center text-accent q-gutter-sm">
            <q-icon size="2em" name="sentiment_dissatisfied" />
            <span>
              {{ message }}
            </span>
            <q-icon size="2em" :name="filter ? 'filter_b_and_w' : icon" />
          </div>
        </template>
        <template v-slot:bottom>
          <q-btn color="primary" label="작업생성" />
          <q-separator vertical />
          <q-checkbox v-model="work_lock" indeterminate-value="maybe" />
          <q-btn color="amber" :label="work_lock ? '잠그기' : '열기'" />
          <q-separator vertical />
          <span class="q-pl-sm">삭제개수</span>
          <q-input v-model="selected.length" type="text" disable dense input-style="width:30px; font-size: 15px;"
            input-class="text-center" />
          <q-btn color="red" label="삭제" />
        </template>
      </q-table>
    </q-card-section>
  </q-card>

  <FileUnitUploadVue :inception="fileModal" :companies="companies" @close="fileModal = false"></FileUnitUploadVue>
  <WorkUnitUploadVue :inception="workModal" :companies="companies" @close="workModal = false"></WorkUnitUploadVue>
</template>

<script>
import { ref } from 'vue'
import FileUnitUploadVue from '../modal/FileUnitUpload.vue';
import WorkUnitUploadVue from '../modal/WorkUnitUpload.vue';

const data = [
  {
    name: 'Frozen Yogurt',
    no: 1101,
    company_name: '에즈금융서비스',
    insure_name: 'ABL생명',
    계정: 20139068,
    work_kind: '수금 자료 다운로드',
    filename: 'CONTRACT_LIST_ALL_C(수금자원관리_해당)',
    schedule: '매일 자정',
    timeout: 0,
    lock: '열림',
    ERP연동: '.',
  },
  {
    name: 'Frozen Yogurt',
    no: 1102,
    company_name: '에즈금융서비스',
    insure_name: 'ABL생명',
    계정: 20139068,
    work_kind: '수금 자료 다운로드',
    filename: 'CONTRACT_LIST_ALL_C(수금자원관리_해당)',
    schedule: '매일 자정',
    timeout: 0,
    lock: '열림',
    ERP연동: '.',
  },
  {
    name: 'Frozen Yogurt',
    no: 1103,
    company_name: '에즈금융서비스',
    insure_name: 'ABL생명',
    계정: 20139068,
    work_kind: '수금 자료 다운로드',
    filename: 'CONTRACT_LIST_ALL_C(수금자원관리_해당)',
    schedule: '매일 자정',
    timeout: 0,
    lock: '열림',
    ERP연동: '.',
  },
];
const pagination = ref({
  sortBy: 'desc',
  descending: false,
  page: 1,
  rowsPerPage: 3,
  rowsNumber: 20
})
const searchForm = ref({
  company: '',
  spec: '',
  insure: '',
  work: '',
  lock: ''
})
const columns = [
  { name: 'No', label: 'No', field: 'no', align: 'center', sortable: true },
  { name: '회사명', label: '회사명', field: 'company_name', align: 'center', sortable: true },
  { name: '보험사', label: '보험사', field: 'insure_name', align: 'center' },
  { name: '계정', label: '계정', field: '계정', align: 'center' },
  { name: '작업', label: '작업', field: 'work_kind', align: 'center' },
  { name: '파일명', label: '파일명', field: 'filename', align: 'center', sortable: true, },
  {
    name: '일정',
    label: '일정',
    field: 'schedule',
    align: 'center',
    sortable: true,
  },
  {
    name: '시간초과',
    label: '시간초과',
    field: 'timeout',
    align: 'center',
    sortable: true,
  },
  {
    name: '잠김',
    label: '잠김',
    field: 'lock',
    align: 'center',
    sortable: true,
    sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
  },
  {
    name: 'ERP연동	',
    label: 'ERP연동	',
    field: 'ERP연동',
    align: 'center',
    sortable: true,
    sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
  },
  {
    name: 'Create',
    label: '',
    field: 'Create',
    align: 'center',
  }
];

export default {
  name: "TableBasic",
  components: { FileUnitUploadVue,WorkUnitUploadVue },
  setup() {
    const show_filter = ref(false)
    const selected = ref([])
    let fileModal = ref(false)
    let workModal = ref(false)

    const FileUnitUpload = () => {
      // 모달에서 닫아도 됨
      inception.value = false
    }
    return {
      FileUnitUpload,
      searchForm,
      selected,
      model: ref(null),
      filter: ref(''),
      pagination,
      companies: [
        '에즈금융서비스', '마이금융파트너'
      ],
      lockCheck: [
        '모두', '열림', '잠김'
      ],
      wokr_kind: [
        '신계약', '수금', '수수료', '모니터링'
      ],
      spec: [
        '생보', '손보'
      ],
      insure: [
        'DB생명', 'DB손보', 'KB생명', 'KB손보', '삼성생명', '삼성화재'
      ],
      show_filter,
      data,
      columns,
      fileModal,
      workModal,
      work_lock: ref(false)
    }
  }
}
</script>

<style scoped >
.rpa-table-nav {
  margin-left: 10px;
}
.rpa-table-nav>div {
  margin-right: 20px;
}
.q-table tbody tr td {
  height: 10px;
}
.q-table .q-table-control {
  justify-content: left;
}
.q-select {
  margin-right: 10px;
  min-width: 150px;
}
.work-rowNum>.q-select {
  min-width: 15px;
  margin-left: 10px;
  padding-top: 3px;
}
.q-table__bottom {
  justify-content: flex-end;
}
.q-table__bottom .q-btn {
  margin: 0 8px;
}
</style>
