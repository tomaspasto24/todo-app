<template>
    <div class="container" id="contenedor" v-if="task.title">
        <div class="row">
            <div class="col-1">
                <div class="form-check form-switch">
                    <input
                        v-if="task.isCompleted"
                        class="form-check-input"
                        type="checkbox"
                        id="flexSwitchCheckDefault"
                        checked
                        @click="changeCheckbox"
                    />
                    <input
                        v-else
                        class="form-check-input"
                        type="checkbox"
                        id="flexSwitchCheckDefault"
                        @click="changeCheckbox"
                    />
                </div>
            </div>
            <div class="col-3">{{ task.title }}</div>
            <div class="col-2">{{ dateFormat }}</div>
            <div class="col-2">
                <button
                    type="button"
                    class="btn btn-danger"
                    @click="deleteTask"
                >
                    Eliminar
                </button>
            </div>
            <div class="col-4">
                <div class="input-group">
                    <button
                        class="btn btn-outline-secondary me-1"
                        type="button"
                        @click="modifyTask"
                    >
                        Modificar
                    </button>
                    <input
                        type="text"
                        class="form-control"
                        aria-describedby="basic-addon1"
                        id="modifyField"
                        v-model="formValue"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            formValue: "",
        };
    },
    props: {
        task: {
            type: Object,
            required: true,
        },
    },
    computed: {
        dateFormat: function () {
            return this.task.date.toLocaleDateString("en-US");
        },
    },
    methods: {
        deleteTask: function () {
            this.$emit("delete", this.task);
        },
        modifyTask: function () {
            if (this.formValue.length !== 0) {
                this.$emit("modify", this.task, this.formValue)
                this.formValue = ''
            }
        },
        changeCheckbox: function () {
            
            this.$emit("refresh", this.task);
        },
    },
};
</script>

<style>
#contenedor {
    background-color: #2d2d2d;
    padding-bottom: 1%;
    border-radius: 0.5rem;
    padding: 1%;
    margin-bottom: 1rem;
}
</style>