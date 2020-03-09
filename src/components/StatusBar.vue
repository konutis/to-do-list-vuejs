<template>
  <div class='status-container'>
    <div v-bind:class='{ "status-item--selected": filterType === "total", "status-item": true }'>
      <button class='status-number' type='button' value='total' v-on:click='onFilter'>
        {{ toDoData.length }}
      </button>
      <p class='status-description'>
        Total
      </p>
    </div>
    <div v-bind:class='{ "status-item--selected": filterType === "remaining", "status-item": true }'>
      <button class='status-number' type='button' value='remaining' v-on:click='onFilter'>
        {{ toDoData.filter(item => item.isDone === false ).length }}
      </button>
      <p class='status-description'>
        Remaining
      </p>
    </div>
    <div v-bind:class='{ "status-item--selected": filterType === "done", "status-item": true }'>
      <button class='status-number' type='button' value='done' v-on:click='onFilter'>
        {{ toDoData.filter(item => item.isDone === true ).length }}
      </button>
      <p class='status-description'>
        Done
      </p>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'StatusBar',
        props: {
            toDoData: {
                type: Array,
                required: true
            },
            filterType: {
                type: String,
                required: true
            }
        },
        methods: {
            onFilter(e) {
                this.$emit('onFilter', e.target.value)
            }
        }
    }
</script>
