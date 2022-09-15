<template>
    <input type="text" v-model="post">
    <button @click="addPost">Add</button>
    <List v-if="posts.length" :posts="posts" @removePost="removePost" @movePost="movePost" />
    <div v-else>
        <img src="../assets/default.jpg" alt="nothing to do">
    </div>
</template>

<script>
import List from '../components/List.vue'
export default {
    components: {List},
    data() {
        return {
            post: "",
            posts: []
        }
    },
    methods: {
        addPost() {
            if(this.post.trim() !== "") { 
                this.posts.push(this.post)
                this.post = ""
            }
        },
        removePost(index) {
            this.posts = this.posts.filter((post, i) => i !== index)
        },
        movePost(index, direction) {
            if(direction.toLowerCase() === 'up') {
                if(!index-1 < 0) {
                    const element = this.posts.splice(index, 1)[0]
                    this.posts.splice(index-1, 0, element)
                }
            }

            if(direction.toLowerCase() === 'down') {
                if(index <= this.posts.length) {
                    const element = this.posts.splice(index, 1)[0]
                    this.posts.splice(index+1, 0, element)
                }
            }
           
        }
    }
}
</script>

<style>

    input {
        padding: 5px;
        width: 300px;
        border-radius: 4px;
        border: none;
        border: 1px solid burlywood
    }

    button {
        padding: 6px;
        width: 50px;
        margin-left: 5px;
        background-color: burlywood;
        color: white;
        border: none;
        cursor: pointer;
        border-radius: 4px;
    }

    button:active {
        background-color: rgb(163, 130, 88);
    }

</style>