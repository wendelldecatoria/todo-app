<template>
    <div class="todo">
        <p class="title is-1 is-spaced">To Do List</p>
        <div class="container">
            <b-field>
                <b-input placeholder="add task" v-model="newTask" @keyup.enter="addTask"></b-input>
            </b-field>
            <div class="buttons">
                <b-button type="is-primary" v-on:click="addTask">Add</b-button>
            </div>

            <ul class="list">
                <li v-for="task in filteredTask" v-bind:key="task.id" v-bind:class="{ completed: task.completed }">
                    <div class="card">
                        <div class="card-content">
                            <p class="subtitle is-size-6"> {{ task.title }} </p>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    let todos = [
        { 'id': 1, 'title': 'Go to the store', 'completed': true },
        { 'id': 2, 'title': 'Go to the Bank', 'completed': false },
        { 'id': 3, 'title': 'Buy Fresh Eggs', 'completed': false }
    ];

    // visibility filters
    var filters = {

        all: function (todos) {
            return todos
        },
        active: function (todos) {
            return todos.filter(function (todo) {
                return !todo.completed
            })
        },
        completed: function (todos) {
            return todos.filter(function (todo) {
                return todo.completed
            })
        }
    }

    export default {
        name: "Todo",
        data() {
            return {
                filter: 'all',
                newTask: '',
                tasks: todos
            }
        },
        methods: {
            addTask() {
                // alert(this.newTask);
                this.tasks.push(
                    {
                        'id': 4,
                        'title': this.newTask,
                        'completed': false
                    }
                )
            },
            updateTask() {

            },
            deleteTask() {

            },

        },
        computed: {
            filteredTask() {
                if(this.filter == 'active') {
                    return filters.active(this.tasks)
                }

                if(this.filter == 'completed'){
                    return filters.completed(this.tasks)
                }

                return filters.all(this.tasks)
            }
        }
    }

</script>

<style scoped>
    .completed {
        text-decoration: line-through;
        opacity: 0.7;
    }
</style>