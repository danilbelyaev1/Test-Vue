<template>

  <div class="container">
    <user-form
        v-model:selectedSort="selectedSort"
        v-model:searchQuery="searchQuery"
        :selectedSort="selectedSort"
        :sortOptions="sortOptions"
        :searchQuery="searchQuery"
    />
    <user-list
        :users="sortedAndSearchUsers"
    />
  </div>

</template>

<script>
import UserForm from "@/components/userForm";
import UserList from "@/components/userList";
export default {
  name: 'App',
  components: {
    UserForm, UserList,
  },
  data(){
    return {
      userList: [],
      selectedSort: '',
      searchQuery: '',
      sortOptions: [
        {value: 'id', name: 'По id'},
        {value: 'city', name: 'По городу'},
      ],
      isLoading: false,
    }
  },
  methods:{
    async fetchUsers () {
      try{
        this.isLoading = true;
        fetch('https://jsonplaceholder.typicode.com/users')
          .then(response => response.json())
          .then(json => {
            this.userList = json
            //Упростим механизм сортировки, вытащив нужные свойства в корень объекта
            this.userList.forEach(user => user.city = user.address.city)
          })

      }
      catch (e) {
        alert('Error')
      } finally {
        this.isLoading = false;
      }
    }
  },
  mounted() {
    this.fetchUsers();
  },
  computed:{
    sortedUsers(){
      return [...this.userList].sort((user1,user2) => {
        return user1[this.selectedSort] ? String(user1[this.selectedSort]).localeCompare(String(user2[this.selectedSort]), "kn", { numeric: true }) : 0
      })
    },
    sortedAndSearchUsers()  {
      return this.sortedUsers.filter(user => user.phone.toLowerCase().replace(/[\-\.\(\)\ ]/g, '').includes(this.searchQuery.replace(/[\-\.\(\)\ ]/g, '').trim().toLowerCase()))
    },
  },
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.container{
  max-width: 1200px;
  margin: 0 auto;
}

</style>
