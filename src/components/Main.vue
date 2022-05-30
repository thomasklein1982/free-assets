<template>
  <div style="width: 100%; height: 100%" :style="{display: 'flex', 'flex-direction': 'column'}">
    <TabView :style="{flex: 1}" style="overflow: hidden">
      <TabPanel header="Free Assets">
        <div style="padding: 0.5rem">
          <p>Version {{$root.version}}</p>
          <p>Diese App erlaubt es dir, freie Grafiken und Sounds für deine Programmierprojekte zu nutzen. Besonders gut geeignet für die Benutzung mit <a style="display: inline" href="https://thomaskl.uber.space/Apps/js-edit/" target="_blank">JSEdit</a> oder <a style="display: inline" href="https://thomaskl.uber.space/Apps/java-app/" target="_blank">JavaApp</a>.
          </p>
          <p>Alle hier zu findenden Assets stehen unter der <a href="https://wiki.creativecommons.org/wiki/De:CC0#:~:text=CC0%20bedeutet%20in%20der%20Palette,der%20Gemeinfreiheit%20(Public%20Domain).&text=Sie%20ist%20genau%20wie%20die,das%20Herzst%C3%BCck%20von%20CC0%20dar." target="_blank">CC0-Lizenz</a> und dürfen somit ohne jegliche Einschränkung verwendet werden.</p> 
          <p>Betreiber dieser App: Thomas Klein (<a href="https://mathe-info.com" target="_blank">mathe-info.com</a>)</p>
        </div>
      </TabPanel>
      <TabPanel header="Grafiken">
        <Chooser type="graphics"></Chooser>
      </TabPanel>
      <TabPanel header="Sounds">
        <Chooser type="sounds"></Chooser>
      </TabPanel>
    </TabView>
  </div>
  
</template>

<script>
import Chooser from "./Chooser.vue";
import Selected from "./Selected.vue";


export default{
  data(){
    return {

    };
  },
  components: {
    Chooser,Selected
  }

}
</script>