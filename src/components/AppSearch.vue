<template>
  <form class="search mb-70">
      <label class="search__label">
          <svg class="search__icon">
              <use xlink:href="./../assets/svg/sprite.svg#icon-search"></use>
          </svg>
          <input type="text" class="search__input js-search-input" placeholder="Поиск по имени" v-model="search" @keyup="getValue()">
      </label>
  <button class="search__reset-button js-search-reset-btn" v-if="btnReset" @click.prevent="reset()">
      <svg class="svg-icons mr-4">
          <use xlink:href="./../assets/svg/sprite.svg#icon-reset"></use>
      </svg>
      Очистить фильтр</button>
  </form>
</template>

<script>
export default {
  name: 'SearchApp',
  props: ['resetBtn', 'users'],
  data: function () {
    return {
      search: '',
      btnReset: false,
      id: 0,
    }
  },
  computed: {
      usersReset() {
        return this.users
      }
  },
  watch: {
    resetBtn(newVal) {
      if(newVal) {
        this.getValue()
      } 
    }
  },
  methods: {
      getValue() {
        if (this.search != '' || this.resetBtn) {
          this.btnReset = true
        } else {
          
          this.btnReset = false
        }

        this.$emit('value', this.search);
      },
      reset() {
        this.search = ''
        this.btnReset = false
        this.$emit('value', this.search);
        this.$emit('reset', this.btnReset);
        this.$emit('users', this.users);
        this.$emit('usersid', this.id);
      }
  },
}
</script>

