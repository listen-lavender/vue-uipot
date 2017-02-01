<template>
    <div>
        <choose v-for="(item, index) in cascade" :curr="index" :next="index+1" :hint="item" @on-select="onSelect">
        </choose>
    </div>
</template>
<script>
    import Choose from './Choose'
    import Vue from 'vue'
    import VueResource from 'vue-resource'
    Vue.use(VueResource)
    export default {
        props: {
            config: {
                type: Object
            }
        },
        data () {
            return {
                cascade: null,
                model: {}
            }
        },
        created(){
            this.loads();
        },
        methods: {
            loads:function(){
                if(this.config.url !== undefined && this.config.url != null){
                    this.$http.get(this.config.url).then((response)=>{
                        this.cascade = response.data.cascade;
                    })
                }
            },
            onSelect:function(next, key, val) {
                // this.$emit('on-modify', key, val);
                this.model[key] = val;
                console.log(this.model);
                if(this.cascade[next] === undefined){
                    ;
                }else{
                    this.cascade[next].param=val;
                    // var obj = {};
                    // this.shallowCopy(this.cascade[next], obj);
                    // Vue.set(this.cascade, next, obj);
                }
            },
            // shallowCopy:function(src, obj) {
            //     for(let key in src)
            //         if(!(key in obj))
            //             obj[key] = src[key];
            //     return obj;
            // }
        },
        components: {
            choose: Choose
        }
    }
</script>
<style>
    
</style>