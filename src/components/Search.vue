<template>
  <div class='search-container'>
    <input
      class='search-input'
      placeholder='Search'
      type='search'
      v-model='searchValue'
      @input='handleSearch'
    >
  </div>
</template>

<script>
    export default {
        name: 'Search',
        props: {
            value: {
                type: String,
                required: false
            }
        },
        data: () => {
            return {
                searchValue: ''
            }
        },
        methods: {
            handleSearch() {
                this.$emit('onSearch', this.searchValue)
            }
        }
    }
</script>
