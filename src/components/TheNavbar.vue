<template>
  <MDBNavbar expand="lg" light bg="light" position="sticky" container="md">
    <MDBNavbarBrand>
      <router-link to="/" class="text-black">МБВ</router-link>
    </MDBNavbarBrand>
    <!-- Toggle button -->
    <MDBNavbarToggler
      target="#navbarRightAlign"
      @click="collapse5 = !collapse5">
    </MDBNavbarToggler>
    <!-- Collapsible wrapper -->
    <MDBCollapse v-model="collapse5" id="navbarRightAlign">
      <MDBNavbarNav right class="mb-2 mb-lg-0">
        <!-- Right links -->
        <MDBNavbarItem to="/">
<!--          <router-link to="/" class="nav-item text-muted">-->
            Главная
<!--          </router-link>-->
        </MDBNavbarItem>
        <!-- Navbar dropdown -->
        <MDBDropdown class="nav-item" v-model="dropdown8" v-if="authLevel === 10000">
          <MDBDropdownToggle
            tag="a"
            class="nav-link"
            @click="dropdown8 = !dropdown8">
            Управление
          </MDBDropdownToggle>
          <MDBDropdownMenu>
            <MDBDropdownItem>
              <router-link class="dropdown-item" to="/calendar">Календарь</router-link>
            </MDBDropdownItem>
            <MDBDropdownItem>
              <router-link class="dropdown-item" to="/appUsers">Пользователи</router-link>
            </MDBDropdownItem>
            <MDBDropdownItem href="#">Служители</MDBDropdownItem>
          </MDBDropdownMenu>
        </MDBDropdown>
        <!-- Right links -->
        <MDBNavbarItem class="me-3 me-lg-0 dropdown">
          <MDBDropdown v-model="dropdown3">
            <MDBDropdownToggle
              tag="a"
              class="nav-link"
              @click="dropdown3 = !dropdown3">
              <MDBIcon icon="user"/>
            </MDBDropdownToggle>
            <MDBDropdownMenu>
              <MDBDropdownItem href="#">Action</MDBDropdownItem>
              <MDBDropdownItem href="#">Another Action</MDBDropdownItem>
              <MDBDropdownItem>
                <router-link to="/accountSettings" class="dropdown-item">Настройки</router-link>
              </MDBDropdownItem>
            </MDBDropdownMenu>
          </MDBDropdown>
        </MDBNavbarItem>
      </MDBNavbarNav>
    </MDBCollapse>
    <!-- Collapsible wrapper -->
  </MDBNavbar>
</template>

<script>
import {
  MDBIcon,
  MDBNavbar,
  MDBNavbarToggler,
  MDBNavbarBrand,
  MDBNavbarNav,
  MDBNavbarItem,
  MDBCollapse,
  MDBDropdown,
  MDBDropdownToggle,
  MDBDropdownMenu,
  MDBDropdownItem,
} from 'mdb-vue-ui-kit'
import {ref} from 'vue'
import axios from '@/axios/dbRequests'
import store from '@/store'

export default {
  components: {
    MDBIcon,
    MDBNavbar,
    MDBNavbarToggler,
    MDBNavbarBrand,
    MDBNavbarNav,
    MDBNavbarItem,
    MDBCollapse,
    MDBDropdown,
    MDBDropdownToggle,
    MDBDropdownMenu,
    MDBDropdownItem,
  },
  setup() {
    const dropdown3 = ref(false)
    const collapse5 = ref(false)
    const dropdown8 = ref(false)
    const authLevel = ref()
    async function getAuthLevel() {
      const {data} = await axios.get(`/appUsers/${store.getters['auth/localId']}/authLevel.json?auth=${store.getters['auth/idToken']}`)
      authLevel.value = +data
    }
    getAuthLevel()
    return {
      collapse5,
      dropdown8,
      dropdown3,
      authLevel,
    }
  },
}
</script>

<style scoped>

</style>