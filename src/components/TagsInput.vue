
<template>
    <div class="tags-input-wrapper">
    <!-- <h2>{{ tags }}</h2> -->
    <span class="tag-item" v-for="(tag,index) in tags" :key="index">
        {{ tag }}
        <a href="#" @click.prevent="removeTag(index)">&times;</a>
    </span>
  
    <input  class="tag-input"
    type="text" 
    v-model.number="newTag"
    @keydown.enter="addNewTag"
    @keydown.tab.prevent="addNewTag"
    @keydown.delete="removeLastTag"
    :class="{'tag-exist':isTagExist}"
    />
    <!-- <button @click="tags.push($event.target.value)">OK</button> -->
</div>
</template>

<script>
export default{
    props:{
        selectedTags:{
            type:Array,
            default:()=>[]
        }
    },
    data(){
        return{
            tags:[...this.selectedTags],
            newTag:''

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
                    this.$emit('change',this.tags)
            
            }
        },
        removeTag(index){
            this.tags.splice(index,1)
            this.$emit('change',this.tags)
        },
        removeLastTag(index){
            if(this.newTag.length === 0){
                this.removeTag(this.tags.length -1)
                this.$emit('change',$this.tags)
            }
        }

    },
    emits:['change']
}
</script>
<style scoped>
.tag-exist{
    color:Red;
    text-decoration:line-through
}
.tags-input-wrapper{
    background: #fff;
    padding:0.5em;
    border: 1px solid #dbdbdb;
    display: flex;
    align-items: center;
    min-height: 36px;
    box-sizing: border-box;
}
.tag-item{
    color:#212529;
    background-color: #eee;
    margin-right: 0.3em;
    padding:0.25em 0.4em;
    font-size: 75%;
    line-height: 1;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding-right: 1.25em;
    padding-left: 0.6em;
}
.tag-input{
    color:#495057;
    flex:1;
    background: transparent;
    border:none;
}
.tag-input:focus{
    outline:none;
}
a.remove-tag{
    text-decoration: ;
}
</style>