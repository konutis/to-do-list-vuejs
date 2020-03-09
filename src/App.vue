<template>
  <div id='app' class='app'>
    <img src='./assets/logo.png' alt='vue' class='logo'>
    <div class='app-container'>
      <header class='app-header'>
        <DateBar />
        <StatusBar
          v-bind:to-do-data='toDoData'
          v-bind:filter-type='filterType'
          @onFilter='onFilter'
        />
      </header>
      <div class='app-body'>
        <Search
          @onSearch='onSearch'
        />
        <div class='list'>
          <ToDoItem
            v-for='(item) in searchList'
            v-bind:id='item.id'
            v-bind:text='item.text'
            v-bind:key='item.id'
            v-bind:is-done='item.isDone'
            @onDelete='onItemDelete'
            @onEdit='onItemEdit'
            @onComplete='onItemComplete'
          />
        </div>
        <button class='add-button' v-on:click='onItemAdd'>
          Add new
        </button>
      </div>

    </div>
    <div class='copyrights'>
      Made by Janis Konutis
    </div>
  </div>
</template>

<script>
    import ToDoItem from './components/ToDoItem'
    import Search from './components/Search'
    import StatusBar from './components/StatusBar'
    import DateBar from './components/DateBar'
    import Helpers from './helpers/helper'
    import './styles/main.scss'

    export default {
        name: 'app',
        components: {
            DateBar,
            StatusBar,
            ToDoItem,
            Search
        },
        data: () => {
            return {
                filterType: 'total',
                search: '',
                toDoData: [
                    {
                        id: '123asd3',
                        text: 'Buy milk',
                        isDone: false
                    },
                    {
                        id: '123a1d3',
                        text: 'Teach Filipp',
                        isDone: true
                    },
                    {
                        id: '124as3d',
                        text: 'Get chick',
                        isDone: false
                    }
                ]
            }
        },
        methods: {
            onItemDelete(id) {
                this.toDoData = this.toDoData.filter((item) => {
                    return item.id !== id
                })
            },
            onItemAdd() {
                this.toDoData.push({
                    id: Helpers.createId(),
                    text: 'New task',
                    isDone: false
                })
            },
            onItemEdit(id, text) {
                const itemIndex = this.toDoData.findIndex((item) => {
                    return item.id === id
                })
                this.toDoData[itemIndex].text = text
            },
            onItemComplete(id, status) {
                const itemIndex = this.toDoData.findIndex((item) => {
                    return item.id === id
                })
                this.toDoData[itemIndex].isDone = status
            },
            onSearch(value) {
                this.search = value
            },
            onFilter(value) {
                this.filterType = value
            }
        },
        computed: {
            searchList() {
                return this.filteredList.filter((item) => {
                    return item.text.toLowerCase().includes(this.search.toLowerCase())
                })
            },
            filteredList() {
                if (this.filterType === 'total') {
                    return this.toDoData
                } else if (this.filterType === 'remaining') {
                    return this.toDoData.filter((item) => {
                        return item.isDone === false
                    })
                } else {
                    return this.toDoData.filter((item) => {
                        return item.isDone === true
                    })
                }

            }
        }
    }
</script>
