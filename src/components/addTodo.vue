<template>
    <div>
        <form @submit="addTodo">
            <input v-model="title" type="text" name="title" placeholder="Add Todo..." >
            <input class="btn" type="submit" value="Add">
        </form>
    </div>    
</template>

<script>
    // import {uuid} from 'vue-uuid'

export default {
    name: "addTodo",
    data() {
        return {
            title: '',
            errorMsg: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault()
            if (this.title === '') {
               this.errorMsg= "Please Enter a Todo"
                this.$emit('emitError', this.errorMsg)
            } else if (!isNaN(this.title)) {
                this.errorMsg= "Your Todo cannot be a number"
                this.$emit('emitError', this.errorMsg)
            }  else {
                 const newTodo = {
                    title: this.title,
                    completed: false
                }
                
                // SEND TO PARENT COMPONENT
                this.$emit('bindTodo', newTodo)
                this.title = ''

            }
            
        }
    }

}
</script>

<style scoped>
    form {
        display: flex
    }
    input[type="text"] {
        padding:5px;
        flex: 10;
    }
    
    input[type="text"] {
        flex: 2;
    }
</style>