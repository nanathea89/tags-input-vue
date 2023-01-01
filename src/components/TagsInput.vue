
<template>
    <h2>{{ tags }}</h2>
    <h5>{{ tags[1].toUpperCase() }}</h5>
    <div v-for="(tag,index) in tags" :key="index">
        {{ tag }}
        <a href="#" @click.prevent="removeTag">&times;</a>
    </div>
    <hr>
    {{ newTag }}
    <br> 
    <input 
    type="text" 
    v-model.number="newTag"
    @keydown.enter="addNewTag"
    @keydown.tab.prevent="addNewTag"
    @keydown.delete="removeLastTag"
    :class="{'tag-exist':isTagExist}"
    />
    <!-- <button @click="tags.push($event.target.value)">OK</button> -->
</template>

<script>
export default{
    data(){
        return{
            tags:['Vue','Angular','React'],
            newTag:'Nuxt'

        }
    },
    watch:{
        newTag(newVal){
            if(newVal.indexOf(',')>-1){
                this.newTag= newVal.slice(0,-1)
                this.addNewTag()
            }
            
        }
    },
    computed:{
        isTagExist(){
            return this.tags.includes(this.newTag.trim())
        }
 
    },
    methods:{
        addNewTag(){
            if(this.newTag.trim() && !this.isTagExist){
                 
                    this.tags.push(this.newTag.trim())
                    this.newTag=''
            
            }
        },
        removeTag(index){
            this.tags.splice(index,1)
        },
        removeLastTag(index){
            if(this.newTag.length === 0){
                this.removeTag(this.tags.length -1)
            }
        }

    }
}
</script>
<style scoped>
.tag-exist{
    color:Red;
    text-decoration:line-through
}
</style>