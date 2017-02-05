<template>
    <div>
        <choose v-for="(item, index) in cascade" :curr="index" :next="index+1" :hint="item" @change="change">
        </choose>
    </div>
</template>
<script>
    import Choose from './Choose'
    export default {
        props: {
            config: {
                type: Object,
                default: {
                    url:null
                }
            }
        },
        data () {
            return {
                cascade: null,
                choice: {}
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
            change:function(next, key, val) {
                this.choice[key] = val;
                var obj = {};
                this.clone(this.choice, obj);
                this.$emit('input', obj);

                this.$emit('change', key, val);

                if(this.cascade[next] === undefined){
                    ;
                }else{
                    this.cascade[next].param=val;
                    // var obj = {};
                    // this.clone(this.cascade[next], obj);
                    // Vue.set(this.cascade, next, obj);
                }
            },
            clone:function(src, obj) {
                for(let key in src)
                    if(!(key in obj))
                        obj[key] = src[key];
                return obj;
            }
        },
        components: {
            choose: Choose
        }
    }
</script>
<style>
    
</style>