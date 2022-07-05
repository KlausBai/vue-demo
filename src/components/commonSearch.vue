<template>
    <div id='common-search-box'>
        <div>{{filter}}</div>
        <div v-for="(service,index) in services" :key="index">{{service}}</div>
    </div>
</template>
<script>
export default {
    name: 'commonSearch',
    props: {
        fetchInitFilter:Function,
        searchService: Function
    },
    data(){
        return {
            filter:{},
            services:[]
        }
    },
    mounted(){
        this.filter = this.fetchInitFilter();
    },
    methods:{
async handleSearch(){
        this.services = await this.searchService(this.filter);
    }
    }
    
}
</script>