<template>
  <q-card>
    <q-card-section class="q-pa-none">
      <q-table
        :rows="data"
        :columns="columns"
        row-key="no"
        :filter="filter"
        v-model:pagination="pagination"
        no-data-label="데이터가 없습니다."
        no-results-label="결과가 없습니다."
        separator="cell"
        hide-bottom
        @row-click="onRowClick"
      >
        <template v-slot:body-cell-변환="props">
          <q-td :props="props">
            <q-btn color="primary" label="변환시작" />
          </q-td>
        </template>
        <template v-slot:top>
          <q-select
            v-model="searchForm.property"
            outlined
            dense
            :options="property"
            label="소유권"
          />
          <q-separator vertical spaced="lg" />
          <q-select
            v-model="searchForm.tag"
            outlined
            dense
            label="태그"
          />
          <q-separator vertical spaced="lg" />
          <q-select
            v-model="searchForm.kind"
            outlined
            dense
            label="종류"
          />
          <q-separator vertical spaced="lg" />
          <q-btn color="brown-5" label="검색" />
          <q-space style="flex-basis: 100%" />
          <q-separator spaced="5px"/>
          <div class="work-info" style="display: flex">
            <span class="q-px-sm work-total" style="padding-top: 13px"
              >total: 1,110건</span
            >
            <q-separator inset="true" />
            <div class="work-pagination q-pt-sm">
              <q-pagination
                v-model="pagination.page"
                :max="5"
                direction-links
                boundary-links
              />
            </div>
            <q-separator inset="true" />
            <div style="display: flex" class="work-rowNum">
              <span style="padding-top: 13px">개수:</span>
              <q-select
                v-model="pagination.rowsNumber"
                :options="[20, 40, 60, 80, 100]"
                dense
              />
            </div>
          </div>
          <q-space />
          <div>
            <q-btn
              color="blue"
              label="등록"
              @click="InsureFileUpload = true"
              class="q-pr-md"
            />
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
      </q-table>
    </q-card-section>
  </q-card>
  <InsureFileUploadModal
    :inception="InsureFileUpload"
    @close="InsureFileUpload=false"
  />
</template>

<script>
import { ref } from "vue";
import InsureFileUploadModal from "../modal/InsureFileUploadModal.vue"

const data = [
  {
    no: 1101,
    ga_name: "에즈금융서비스",
    insure_name: "ABL생명",
    계정: 20139068,
    work_kind: "수금 자료 다운로드",
    file_code: "123ABC",
    created_time: "2022-06-09",
  },
];
const pagination = ref({
  sortBy: "desc",
  descending: false,
  page: 1,
  rowsPerPage: 3,
  rowsNumber: 20,
});
const searchForm = ref({
  property: "",
  tag: "",
  kind: "",
});
const columns = [
  { name: "No", label: "No", field: "no", align: "center", sortable: true },
  {
    name: "GA",
    label: "GA",
    field: "ga_name",
    align: "center",
    sortable: true,
  },
  { name: "보험사", label: "보험사", field: "insure_name", align: "center" },
  { name: "계정", label: "계정", field: "계정", align: "center" },
  { name: "작업", label: "작업", field: "work_kind", align: "center" },
  {
    name: "작업구분",
    label: "작업구분",
    field: "work_kind",
    align: "center",
    sortable: true,
  },
  {
    name: "파일코드",
    label: "파일코드",
    field: "file_code",
    align: "center",
    sortable: true,
  },
  {
    name: "생성시간",
    label: "생성시간",
    field: "created_time",
    align: "center",
    sortable: true,
  },
  {
    name: "파일다운로드",
    label: "파일다운로드",
    field: "file_download",
    align: "center",
  },
  {
    name: "변환",
    label: "변환",
    field: "translation",
    align: "center",
  },
];

export default {
  name: "WorkManagementTable",
  components: {InsureFileUploadModal},
  setup() {
    const show_filter = ref(false);
    let InsureFileUpload = ref(false);
    const onRowClick = (evt, row, index) =>{
      // workDetailModal.value = true
      // detail.value = row
    }
    const FileUnitUpload = () => {
      // 모달에서 닫아도 됨
      inception.value = false;
    };
    return {
      FileUnitUpload,
      onRowClick,
      InsureFileUpload,
      searchForm,
      model: ref(null),
      filter: ref(""),
      pagination,
      show_filter,
      data,
      columns,
      property: ['글로벌금융판매','인카','온에셋']
    };
  },
};
</script>

<style scoped>
.rpa-table-nav {
  margin-left: 10px;
}
.rpa-table-nav > div {
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
.work-rowNum > .q-select {
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
