<script >
// import TagsInput from './components/TagsInput.vue'
export default{
  // components: { TagsInput },
  data(){
    return{
      listTags:['Vue','React','Angular:']
    }
  }
  
}

</script>

<template>
  <div>
   <h1>Hello</h1>
   {{ listTags }}
   <tags-input :selectedTags="listTags"></tags-input>
   <tags-input :selectedTags="listTags"></tags-input>
   <hr/>
    
  </div>
 
</template>

<style >
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
