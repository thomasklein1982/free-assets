<template>
  <div style="display: inline-block; text-align: center; margin: 0.5rem; overflow: hidden" :style="{height: (size+2)+'rem', border: selected? '2pt dashed gold':''}">
    <div @click="click()" style="width: 100%; height: 100%">
      <audio  controls style="height: calc(100% - 2rem)" v-if="type==='sounds'" :src="'https://thomaskl.uber.space/Webapps/Assets/'+asset.path"/>
      <img v-else style="height: calc(100% - 2rem)" :src="'https://thomaskl.uber.space/Webapps/Assets/'+asset.path">
      <div style="font-size: small">{{asset.name}}</div>
    </div>
    
    
  </div>
  
</template>

<script>
export default{
  props: {
    asset: Object,
    size: Number,
    selected: Boolean,
    type: String
  },
  data(){
    return {
      
    }
  },
  methods: {
    click(){
      if(this.selected){
        this.$emit("deselect");
      }else{
        this.$emit("select");
      }
      
    }
  }
}
</script>