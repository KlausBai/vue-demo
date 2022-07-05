<template>
    <div id='set-label-box'>
        <input v-model="serviceId"/>
        <div style="width:100px;height:100px;" @click="handleClickQuery">搜</div>
        <input v-model="label"/>
        <div style="width:100px;height:100px;" @click="handleClickSet">设定</div>
    </div>
</template>
<script>
export default {
    name: 'setServiceLabel',
    props: {
        init:Function,
        setServiceLabelService:Function,
        getServiceLabelService: Function
    },
    data(){
        return {
            serviceId: '',
            label: ''
        }
    },
    mounted(){
        const el = document.getElementById('set-label-box')
        this.init(el);
    },
    methods:{
        async handleClickQuery(){
        console.log('handleClickQuery');
        this.label = await this.getServiceLabelService(this.serviceId)
        console.log(this.label)
        },
        handleClickSet(){
            console.log('handleClickSet');
            this.getServiceLabelService(this.serviceId,this.label)
        }
    }
    
}
</script>