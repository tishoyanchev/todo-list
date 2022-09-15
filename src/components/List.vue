<template>
    <div class="container">
        <div class="list-wrapper">
          <div v-for="(post, index) in posts" :key="index" class="post-wrapper" @mouseenter="handleMovePost" @mouseleave="handleMovePost"> 
            <div class="post">
                <span class="post__index">{{index+1}}.</span>
                <span>{{post}}</span>
            </div>
            <div class="movePost" v-if="showArrows && showPostIndex === index">
                <span v-if="index !== 0"  @click="$emit('movePost', index, 'up'); toggleShowArrows()">
                    <font-awesome-icon  icon="fa-solid fa-arrow-up" />
                </span>
                <span v-if="index !== posts.length-1"  @click="$emit('movePost', index, 'down'); toggleShowArrows()">
                    <font-awesome-icon  icon="fa-solid fa-arrow-down" />
                </span>
                <span class="close__icon" @click="$emit('removePost', index)">X</span>
            </div>
          </div>
        </div>
    </div>
</template>

<script>

export default {
    props: ['posts'],
    data() {
        return {
            showArrows: false,
            showPostIndex: null,
            secondHover: false
        }
    },
    methods: {
        handleMovePost(e) {
            this.showPostIndex = parseInt(e.target.firstElementChild.firstElementChild.innerHTML) -1
        
            if(e.type.toLowerCase() === 'mouseenter') {
                this.showArrows = true
            }
            if(e.type.toLowerCase() === 'mouseleave') {
                this.showArrows = false
            }

            if(this.secondHover && e.type.toLowerCase() === 'mouseenter') {
                this.secondHover = false
                this.showArrows = !this.showArrows
            }
        },
        toggleShowArrows() {
            const movedElement = document.querySelector('.movePost').closest('.post-wrapper')
            this.secondHover = true;
            this.showArrows = !this.showArrows
            let evt = new MouseEvent("mouseleave");
            movedElement.dispatchEvent(evt);
        }
    }
}
</script>

<style>

    .post-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 5px;
        margin-bottom: 5px;
        margin-left: 0;
        position: relative;
    }

    .post {
        padding: 5px 10px;
        border: 1px solid #ddd;
        background-color: burlywood;
        color: white;
        border-radius: 4px;
    }

    .movePost {
        display: flex;
        align-items: center;
        height: 100%;
        margin-left: 5px;
    }

    .movePost span {
        margin: 0 3px;
        background-color: burlywood;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .movePost span:hover {
        cursor: pointer;
    }

    .close__icon {
        cursor: pointer;
    }

    .post__index {
        margin-right: 5px;
    }
    
    .list-wrapper {
        width: 60%;
        padding-inline-start: 0;
    }

    .container {
        margin-top: 30px;
        display: flex;
        justify-content: center;
    }

</style>