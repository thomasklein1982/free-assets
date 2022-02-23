<template>
  <Dialog :closable="false" header="Assets exportieren" :visible="show"> 
    <div style="padding: 0.5rem">
      Wie sollen die Assets exportiert werden? <Dropdown v-model="mode" :options="modes" optionLabel="label" optionValue="value"/>
    </div>
    <textarea style="height: 7rem" id="textarea" :value="code"></textarea>
    <template #footer>
      <Button class="copy" data-clipboard-target="textarea" label="Kopieren" icon="pi pi-copy" autofocus />
      <Button @click="close()" label="Abbrechen" icon="pi pi-times" class="p-button-text"/>
    </template>
  </Dialog>

</template>
<script>
export default {
  data(){
    return {
      show: false,
      name: '',
      assets: null,
      mode: 1,
      modes: [
        {label: "als URLs", value: 1},
        {label: "für JSEdit", value: 2},
        {label: "für JavaApp", value: 3}
      ]
    }
  },
  computed: {
    code(){
      console.log(this.mode)
      let s="";
      for(let i=0;i<this.assets.length;i++){
        let a=this.assets[i];
        let url="https://thomaskl.uber.space/Webapps/Assets/"+a.path;
        if(this.mode===1){
          s+=url;
        }else{
          if(this.mode===3){
            s+="App.";
          }
          s+="loadAsset("+JSON.stringify(url)+","+JSON.stringify(a.name)+")"
        }
        s+="\n";
      }
      return s;
    }
  },
  methods: {
    open(assets){
      this.show=true;
      this.assets=assets;
    },
    close(){
      this.show=false;
    },
    confirm(){
      this.$emit('ok',this.name);
      this.name="";
      this.close();
    }
  }
}
</script>
<style scoped>
  .p-field * {
    display: block;
  }
</style>