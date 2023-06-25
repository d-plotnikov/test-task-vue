<template>
    <main>
        <section class="container">
            <h1 class="h1 mb-20 mt-12">Список пользователей</h1>

            <AppSearch :search="search" @value="search = $event" :reset-btn="resetBtn" @reset="resetBtn = $event" :users="cloneUserData" @users="userData = $event" @usersid="idItem = $event"/>
            <AppSortable :users="userByName" @users="userData = $event" @reset="resetBtn = $event"/>
            <UserList :users="users" @delete="idItem = $event" :page="page" @page="page = $event" @update="userData = $event"/>
            <AppPagination :page="page" @paginate="page = $event" :count="countUsers" :per-page="userPerPage"/>

        </section>
    </main>



</template>

<script>
import AppSearch from './components/AppSearch.vue'
import AppSortable from './components/AppSortable.vue'
import UserList from './components/UserList.vue'
import AppPagination from './components/AppPagination.vue'

export default {
  name: 'App',
  components: { AppSearch, AppSortable, UserList, AppPagination },
  data() {
    return {
        userData: [],
        cloneUserData: [],
        page: 1,
        userPerPage: 5,
        search: '',
        idItem: 0,
        openModal: false,
        resetBtn: false 
    };
  },
  watch: {
      userByName() {
        if(this.search != ''){
            this.page = 1
        }
      }
  },
  computed: {
      userItems() {
        return this.deleteItemArray()
      },
      userByName() {
          return this.userItems.filter(item => item.username.toLowerCase().includes(this.search.toLowerCase()))
      },
      users(){
          const offset = (this.page - 1) * this.userPerPage
          return this.userByName.slice(offset, offset + this.userPerPage)
      },
      countUsers() {
          return this.userByName.length
      },
  },
  methods: {
    deleteItemArray() {
        this.userData = this.userData.filter(item => item.id != this.idItem)
        return this.userData
    },

  },
  beforeMount() {

      fetch('https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users')
        .then(response => response.json())
        .then(json => {
          this.userData = json
          this.cloneUserData = json
        })

  },
}
</script>

