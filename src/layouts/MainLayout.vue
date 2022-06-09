<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          icon="menu"
          aria-label="Menu"
        />
        <q-toolbar-title>
          {{$route.name}}
        </q-toolbar-title>
        <q-space/>
        <div class="q-gutter-sm row items-center no-wrap">

        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-primary text-white"
      width="200"
    >
      <q-list>
        <!-- <q-expansion-item
          icon="pages"
          label="Pages"      >
          <q-list class="q-pl-lg">
            <q-item to="/Login-1" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="email"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Login-1</q-item-label>
              </q-item-section>
            </q-item>
            <q-item to="/Lock" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="lock"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Lock Screen</q-item-label>
              </q-item-section>
            </q-item>
            <q-item to="/Lock-2" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="lock"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Lock Screen - 2</q-item-label>
              </q-item-section>
            </q-item>
            <q-item to="/Pricing" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="list"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Pricing</q-item-label>
              </q-item-section>
            </q-item>
            <q-item-label header class="text-weight-bolder text-white">Generic</q-item-label>
            <q-item to="/Profile" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="person"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>User Profile</q-item-label>
              </q-item-section>
            </q-item>
            <q-item to="/Maintenance" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="settings"/>
              </q-item-section>
              <q-item-section>
                <q-item-label>Maintenance</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-expansion-item> -->
        <q-item to="/WorkSchedule" active-class="my-menu-link" :active="link === 'workSchedule'" @click="link = 'workSchedule'">
          <q-item-section avatar>
            <q-icon name="event_available"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>작업일정</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="#" active-class="my-menu-link" :active="link === 'insureData'" @click="link = 'insureData'">
          <q-item-section avatar>
            <q-icon name="inventory"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>보험사자료</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="#" active-class="my-menu-link" :active="link === 'rpaHistory'" @click="link = 'rpaHistory'">
          <q-item-section avatar>
            <q-icon name="history"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>RPA작업이력</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/InsureFile" active-class="my-menu-link" :active="link === 'insureFile'" @click="link = 'insureFile'">
          <q-item-section avatar>
            <q-icon name="folder"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>보험사 파일</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/WorkerManagement" active-class="my-menu-link" :active="link === 'workerManagement'"  @click="link = 'workerManagement'">
          <q-item-section avatar>
            <q-icon name="screen_search_desktop"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>작업자관리</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'workManagement'"  @click="link = 'workManagement'">
          <q-item-section avatar>
            <q-icon name="build"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>작업관리</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'monitoring'"  @click="link = 'monitoring'">
          <q-item-section avatar>
            <q-icon name="monitor"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>모니터링</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'account'"  @click="link = 'account'">
          <q-item-section avatar>
            <q-icon name="people"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>계정</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'messageHistory'"  @click="link = 'messageHistory'">
          <q-item-section avatar>
            <q-icon name="settings_cell"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>문자수신이력</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'customerManagement'"  @click="link = 'customerManagement'">
          <q-item-section avatar>
            <q-icon name="manage_accounts"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>회원관리</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'report'"  @click="link = 'report'">
          <q-item-section avatar>
            <q-icon name="bug_report"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>결과 보고서</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'gaNotice'"  @click="link = 'gaNotice'">
          <q-item-section avatar>
            <q-icon name="notifications"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>GA공지</q-item-label>
          </q-item-section>
        </q-item>
        <q-item to="/#" active-class="my-menu-link" :active="link === 'gaLink'"  @click="link = 'gaLink'">
          <q-item-section avatar>
            <q-icon name="link"/>
          </q-item-section>
          <q-item-section>
            <q-item-label>GA/보험사 링크</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container class="bg-grey-2">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'
import Messages from "./Messages";

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
    Messages
  },

  setup () {
    const leftDrawerOpen = ref(false)
    return {
      link: ref('workSchedule'),
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      changeTitle (value) {
          title.value = value
      },
    }
  }
})
</script>
<style lang="sass">
.my-menu-link
  color: #00FFFF
</style>
