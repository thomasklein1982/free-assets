<template>
  <div :style="{display: 'flex', 'flex-direction': 'column', flex: 1}" style="padding: 0.5rem; width: 100%; overflow: hidden">
    <div :style="{alignItems: 'center', display: 'flex'}">
      <InputText placeholder="Suchbegriffe eingeben" :style="{flex: 1}" v-model="search"/>
      <Slider style="width: 14rem" v-model="size"/>
      <Button @click="clickExport()" label="Exportieren"/>
    </div>
    <div :style="{flex: 1}" style="overflow: auto">
      <template v-for="(a,i) in selected">
        <ImageButton :type="type" @deselect="deselect(a)" :selected="true" :size="realSize" :asset="a"/>
      </template>
      <template v-for="i in perPage">
        <ImageButton :type="type" @select="selected.push(assets[i-1+(page-1)*perPage])" :selected="false" :size="realSize" v-if="i-1+(page-1)*perPage<assets.length"  :asset="assets[i-1+(page-1)*perPage]"/>
      </template>
    </div>
    <div :style="{display: 'flex'}">
      <Button :disabled="page===1" icon="pi pi-chevron-left" @click="clickBack()"/>
      <div :style="{flex: 1}" style="text-align: center" >Seite {{page}}</div>
      <Button :disabled="!more" icon="pi pi-chevron-right" @click="clickNext()"/>
    </div>
    
  </div>
  <DialogExport ref="dialogExport"/>
</template>

<script>
import {assets} from "../asset-paths.js";
import ImageButton from "./ImageButton.vue";
import DialogExport from "./DialogExport.vue";

export default{
  props: {
    type: String
  },
  data(){
    return {
      search: "",
      page: 1,
      perPage: 20,
      size: 40,
      more: false,
      selected: []
    };
  },
  watch: {
    search(){
      this.page=1;
    }
  },
  computed: {
    realSize(){
      return (this.size+1)*0.1
    },
    assets(){
      this.more=false;
      let array=[];
      let words=this.search.split(/[ ,;]+/);
      for(let i=0;i<assets[this.type].length;i++){
        let a=assets[this.type][i];
        if(this.isSelected(a)) continue;
        let okay=a.name.indexOf(this.search)>=0;
        if(a.tags){
          for(let j=0;j<a.tags.length;j++){
            let tag=a.tags[j];
            for(let k=0;k<words.length;k++){
              let w=words[k];
              if(w.length>0 && tag.indexOf(w)>=0){
                okay=true;
                break;
              }
            }
          }
        }
        if(okay){
          if(array.length>=this.page*this.perPage){
            this.more=true;
            return array;
          }
          array.push(a);
        }
        
      }
      return array;
    }
  },
  methods: {
    clickBack(){
      if(this.page>1){
        this.page--;
      }
    },
    clickNext(){
      if(this.more){
        this.page++;
      }
    },
    deselect(asset){
      for(let i=0;i<this.selected.length;i++){
        let a=this.selected[i];
        if(a.path===asset.path){
          this.selected.splice(i,1);
          return;
        }
      }
    },
    isSelected(asset){
      return this.selected.indexOf(asset)>=0;
    },
    clickExport(){
      this.$refs.dialogExport.open(this.selected);
    }
  },
  components: {
    ImageButton, DialogExport
  }
}
</script>