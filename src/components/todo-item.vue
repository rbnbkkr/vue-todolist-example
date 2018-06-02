<template>
    <li>
        <div class="todo">
            <input class="checkbox" type="checkbox" :checked="todo.completed"
                   @change="$emit('changeStatusTodo', {'id': todo.id, 'completed': $event.target.checked } )">

            <label>
                {{ todo.title }}
            </label>
            <button class="button is-small is-danger" @click="$emit('removeTodo', todo.id)">
                <span class="icon">
                    <i class="fas fa-trash-alt"></i>
                </span>
            </button>
        </div>
    </li>
</template>

<script>
    export default {
        name: "todo-item",
        props: {
            todo: Object
        }
    }
</script>

<style scoped>

</style>