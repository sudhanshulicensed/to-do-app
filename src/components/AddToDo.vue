<template>
<div class="whole">
    
    <div class="overlay" v-if="show" >
        <div class="content">
                <form v-on:submit.prevent>
                    <label for="context">What are you up for?</label>
                    <input v-model="subject.content" id="context" type="text">
                    <button v-if="!editObjc" @click="addMyTask">Add Task</button>
                    <button v-else @click="editMyTask">Edit Task</button>
                </form>
                <button @click="closeModal">Cancel</button>
        </div> 
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
        },
    },
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

    .overlay{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.6);
        backdrop-filter: blur(3px);
        z-index: 5;
    }
</style>