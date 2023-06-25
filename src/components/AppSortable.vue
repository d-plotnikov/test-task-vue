<template>
    <div class="sortable">
        <div class="sortable__description">Сортировка:</div>
        <button class="sortable__button sortable__button_active js-sortable-btn-date" @click="sortableDate()">Дата регистрации</button>
        <button class="sortable__button js-sortable-btn-rating" @click="sortableRating()">Рейтинг</button>
    </div>
</template>

<script>
export default {
  name: 'AppSortable',
  props: ['users'],
  data: function () {
      return {
          sortMinDate: false,
          sortMinRating: false,
          resetBtn: false
      }
  },
  computed: {
    getUsers() {
      return this.users
    }
  },
  methods: {
    numberFormat(arr) {
        arr = Number(arr.split('T')[0].split('-').join(''))
        return arr
    },
    sortableDate() {
      this.resetBtn = true
      if(!this.sortMinDate) {
        this.getUsers.sort((a, b) => { 
            if (this.numberFormat(a.registration_date) > this.numberFormat(b.registration_date)) return -1 
        })
        this.sortMinDate = true
      } else {
        this.getUsers.sort((a, b) => { 
            if (this.numberFormat(a.registration_date) < this.numberFormat(b.registration_date)) return -1 
        })
        this.sortMinDate = false
      }

      this.$emit('users', this.getUsers);
      this.$emit('reset', this.resetBtn);
      
      
    },
    sortableRating() {
      this.resetBtn = true
      if(!this.sortMinRating) {
        this.getUsers.sort((a, b) => {
              if(a.rating > b.rating) return -1
        })
        this.sortMinRating = true
      } else {
        this.getUsers.sort((a, b) => {
              if(a.rating < b.rating) return -1
        })
        this.sortMinRating = false
      }

      this.$emit('users', this.getUsers);
      this.$emit('reset', this.resetBtn);
    }
  },

}
</script>
