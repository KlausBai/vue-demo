<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div class="first">
    <compSele v-bind="dataMap['first']"/>
  </div>
  <div class="second">
    <compSele v-bind="dataMap['second']"/>
  </div>
  <div class="third">
    <compSele v-bind="dataMap['third']"/>
  </div>
</template>

<script>
import compSele from './components/compSele.vue'
import { backendConfig } from './config'
const fetchBackEndConfig = async ()=>{
  /** 模拟从后台获取数据 */
  return backendConfig;
}
const serviceLabelMap = {}
export default {
  name: 'App',
  components: {
    compSele
  },
  data(){
    return {
      dataMap: {}
    }
  },
  async mounted(){
    const endConfig = await fetchBackEndConfig();
    this.dataMap = endConfig.reduce((previous, {blockName,functionName}) => {
      previous[blockName] = {
        funcName: functionName,
        compData:this.initFuncData(functionName)
      };
      return previous
    }, {})
  },
  methods:{
    initFuncData(funcName){
      switch (funcName) {
        case 'setServiceLabel':{
          const init = (el)=> {
            if(el.style && el.style.background){
              el.style.background = 'white'
            }
          }
          const setServiceLabelService = async (serviceId,label) => {
            serviceLabelMap[serviceId] = label;
          }
          const getServiceLabelService = async (serviceId) => {
            return serviceLabelMap[serviceId] || 'default';
          }
          return {
            init,
            setServiceLabelService,
            getServiceLabelService
          }
        }
          
        case 'commonSearch': 
          {
            const fetchInitFilter = async ()=> {
            return {
                serviceType: 1
              }
            }
            const searchService = async (filter)=>{
              if(filter.serviceType === 1) return [
                {serviceName: '卓动服务'}
              ]
              else return []
            }
            return {
              fetchInitFilter,
              searchService
            }
          }
          default:
            return {}
        /** addSolution就不写了 */
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
