<template>
    <div class="backdrop" v-if="show">
        <div class="content">
                <form v-on:submit.prevent>
                    {{ editObjc }}
                    <label for="context">What are you up for?</label>
                    <input v-model="subject.content" id="context" type="text">
                    <button v-if="!editObjc" @click="addMyTask">Add Task</button>
                    <button v-else @click="editMyTask">Edit Task</button>
                </form>
                <button @click="closeModal">Cancel</button>
        </div>        
    </div>
</template>

<script>
export default {
    name: "AddToDo",
    props: {
        editObjc: {
            type: String,
            default: null,
        },
        show: {
            type: Boolean,
        }
    },
    watch: {
        editObjc (newVal) {
            this.subject.content = newVal;
            console.log(newVal)
        }
    },
    data(){
        return {
            subject: {
                content: "",
            },
            close: false,
            isEdit: false,
        }
    },
    methods: {
        addMyTask() {
            this.$emit("myTask", this.subject);
            this.subject.content = "";
            this.closeModal();
        },
        editMyTask() {
            console.log(this.subject)
            this.$emit("myTaskEdit", this.subject);
            this.subject.content = "";
            this.closeModal();
        },

        closeModal() {
            this.$emit("close");
        }
    }
}
</script>

<style scoped>

    .content{
        box-sizing: border-box;
        margin: 50px auto;
        width: 400px;
        margin: 20px;
        padding: 20px;
        background: white;
        border-radius: 10px;
    }

    .backdrop{
        position: fixed;
        padding: 100px;
        background: rgba(0, 0, 0, 0.6);
        width: 100vh;
        height: 100vh;
    }
</style>