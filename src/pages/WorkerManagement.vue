<template>
  <q-card-section>
      <div class="rpa-table-nav">
        <q-tabs v-model="tab" align="left">
          <q-tab name="작업자관리" label="작업자관리" />
          <q-tab name="작업관리" label="작업관리" />
        </q-tabs>
      </div>
    </q-card-section>
     <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="작업자관리">
            <tables-work-management></tables-work-management>
          </q-tab-panel>
          <q-tab-panel name="작업관리">
            <table-actions></table-actions>
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
    TableActions: defineAsyncComponent(() => import('components/tables/TableActions')),
    TablesWorkManagement: defineAsyncComponent(() => import('components/tables/WorkManagementTable'))
  },
  setup() {
    return {
      tab:ref('작업자관리')
    }
  }
})
</script>

<style>

</style>
