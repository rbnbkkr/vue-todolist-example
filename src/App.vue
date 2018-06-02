<template>
    <div id="app" class="container">
        <div class="card">
            <div class="card-header">
                <div class="card-header-title is-centered">Todo list</div>
            </div>
            <div class="card-content">
                <div class="field has-addons">
                    <div class="control is-expanded">
                        <input class="input" type="text" placeholder="New todo.." v-model="newTodo"
                               @keyup.enter="addTodo">
                    </div>
                    <div class="control">
                        <button class="button is-info" @click="addTodo">
                            Add
                        </button>
                    </div>
                </div>
            </div>
            <div class="card-content" v-if="uncompletedTodos.length > 0">
                <h4>Todo</h4>
                <ul class="todo-list">
                    <todo-item v-for="(todo, index) in uncompletedTodos" :key="'uncompleted'+index"
                               :todo="todo" @changeStatusTodo="changeStatusTodo" @removeTodo="removeTodo"></todo-item>
                </ul>
            </div>
            <div class="card-content" v-if="completedTodos.length > 0">
                <h4>Completed</h4>
                <ul class="todo-list">
                    <todo-item v-for="(todo, index) in completedTodos" :key="'completed'+index" class="removed"
                               :todo="todo" @changeStatusTodo="changeStatusTodo" @removeTodo="removeTodo"></todo-item>
                </ul>
            </div>
        </div>

    </div>
</template>

<script>
    import TodoItem from './components/todo-item'

    export default {
        name: 'App',

        components: {
            'todo-item': TodoItem
        },

        data() {
            return {
                todos: [
                    {
                        id: 1,
                        title: 'Grocery shopping',
                        completed: false
                    },
                    {
                        id: 2,
                        title: 'Mow the lawn',
                        completed: false
                    },
                    {
                        id: 3,
                        title: 'Clean up room',
                        completed: false
                    },
                    {
                        id: 4,
                        title: 'Write a blog article',
                        completed: true
                    }
                ],
                autoIncrement: 5,
                newTodo: ''
            }
        },

        computed: {
            completedTodos() {
                return this.todos.filter(todo => {
                    return todo.completed === true
                })
            },
            uncompletedTodos() {
                return this.todos.filter(todo => {
                    return todo.completed === false
                })
            }
        },

        methods: {
            addTodo() {
                if (this.newTodo.trim() == '') {
                    return
                }

                this.todos.push({
                    id: this.autoIncrement++,
                    title: this.newTodo,
                    completed: false
                })

                this.newTodo = ''
            },
            removeTodo(id) {
                if (confirm('Are you sure you want to remove this todo?')) {
                    this.todos = this.todos.filter(todo => {
                        return todo.id !== id
                    })
                }
            },
            changeStatusTodo(changedStatus) {
                var todo = this.todos.find(todo => todo.id === changedStatus.id)
                todo.completed = changedStatus.completed
            }
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        margin-top: 60px;
        width: 600px;
    }

    .card-content h4 {
        text-align: center;
        font-weight: 700;
    }

    input.checkbox {
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto 0;
    }

    .todo {
        position: relative;
        min-height: 42px;
        border-bottom: 1px solid #ddd;
    }

    .todo label {
        display: block;
        margin-left: 20px;
        padding: 10px 40px 10px 10px;
        color: #999;
        font-size: 1rem;
    }

    .todo .button.is-danger {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        margin: auto 0;
    }

    .removed label {
        text-decoration: line-through;
    }

</style>
