<template>
  <q-card-section>
      <div class="rpa-table-nav">
        <q-tabs v-model="tab" align="left">
          <q-tab name="작업일정" label="작업일정" />
          <q-tab name="보험사자료" label="보험사자료" />
          <q-tab name="RPA작업이력" label="RPA작업이력" />
        </q-tabs>
      </div>
    </q-card-section>
     <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="작업일정">
            <tables-basic></tables-basic>
          </q-tab-panel>
          <q-tab-panel name="보험사자료">
            <table-actions></table-actions>
          </q-tab-panel>
          <q-tab-panel name="RPA작업이력">
            <table-dark-mode></table-dark-mode>
          </q-tab-panel>
        </q-tab-panels>
    <!-- <table-progress></table-progress>
    <table-custom-grid></table-custom-grid> -->
</template>

<script>
import {defineComponent, defineAsyncComponent,ref} from 'vue';

export default defineComponent({
  name: "Tables",
  components: {
    TableProgress: defineAsyncComponent(() => import('components/tables/TableProgress')),
    TableCustomGrid: defineAsyncComponent(() => import('components/tables/TableCustomGrid')),
    TableDarkMode: defineAsyncComponent(() => import('components/tables/TableDarkMode')),
    TableActions: defineAsyncComponent(() => import('components/tables/TableActions')),
    TablesBasic: defineAsyncComponent(() => import('components/tables/TableRPA'))
  },
  setup() {
    return {
      tab:ref('작업일정')
    }
  }
})
</script>

<style>

</style>
