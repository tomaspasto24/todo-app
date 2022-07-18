<template>
    <div>
        <div class="container" id="principal">
            <input
                class="form-control form-control-lg"
                type="text"
                placeholder="Add task"
                aria-label=".form-control-lg"
                id="agregar"
                @keyup.enter="addTask($event)"
            />

            <task-item
                v-for="(item, index) in noCompleted"
                :key="index"
                :task="item"
                @delete="deleteTask"
                @modify="modifyItem"
                @refresh="refresh"
            ></task-item>
        </div>

        <h2>Historial de Tareas</h2>

        <div class="container" id="principal">
            <task-item
                v-for="(item, index) in completed"
                :key="index"
                :task="item"
                @delete="deleteTask"
                @modify="modifyItem"
                @refresh="refresh"
            ></task-item>
        </div>
    </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
    data: function () {
        return {
            tasks: [],
        };
    },
    components: {
        TaskItem,
    },
    methods: {
        addTask: function (event) {
            event.preventDefault();
            var titleTask = event.target.value;
            var task = {
                title: titleTask,
                date: new Date(),
                isCompleted: false,
                id: Math.random(),
            };
            this.tasks = [...this.tasks, task];
            event.target.value = "";
        },
        deleteTask: function (taskToDelete) {
            this.tasks = this.tasks.filter(
                (task) =>
                    task.title !== taskToDelete.title ||
                    task.id !== taskToDelete.id
            );
        },
        modifyItem: function (taskToModify, newTitle) {
            taskToModify.title = newTitle;
        },
        refresh: function (taskToChange) {
            taskToChange.isCompleted = !taskToChange.isCompleted;
            // this.$forceUpdate();
        },
    },
    computed: {
        noCompleted: function () {
            return this.tasks.filter((task) => !task.isCompleted);
        },
        completed: function () {
            return this.tasks.filter((task) => task.isCompleted);
        },
    },
};
</script>

<style>
.container {
    margin-bottom: 5%;
}
#agregar {
    margin-bottom: 5%;
}
</style>