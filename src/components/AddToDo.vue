<template>
    <div class="content">
        <form v-on:submit.prevent>
            <label for="context">What are you up for?</label>
            <input v-model="subject.content" id="context" type="text">
            <button @click="addMyTask">Add Task</button>
        </form>
    </div>
</template>

<script>
export default {
    name: "AddToDo",
    data(){
        return {
            subject: {
                content: "",
            },
        }
    },
    methods: {
        addMyTask() {
            this.$emit("myTask", this.subject);
            this.subject.content = "";
        }
    }
}
</script>

<style>
    .content{
        /* position: absolute; */
        /* width: 300px; */
        /* height: auto; */
        /* margin: 10px; */
    }
</style>