<template>
    <div>
      <label>{{hint.label}}</label>
      <select v-model="choice">
        <option v-for="option in options" :value="option.value">
          {{option.text}}
        </option>
      </select>
    </div>
</template>
<script>
    export default {
        props: {
            curr: {
                type: Number,
            },
            next: {
                type: Number,
            },
            hint: {
                type: Object,
                default: {
                    url:null,
                    label:null,
                    param:null,
                    name:null
                }
            }
        },
        data () {
            return {
                options: null,
                choice: null
            }
        },
        watch: {
            'hint.param':function(newVal, oldVal) {
                if(newVal && newVal != oldVal){
                    this.loads();
                }
            },
            'choice':function(newVal, oldVal) {
                if(newVal != oldVal){
                    this.$emit("on-select", this.next, this.hint.name, this.choice);
                }
            },
        },
        created(){
            this.loads();
        },
        methods: {
            loads:function(){
                if(this.hint.param !== undefined && this.hint.param != null){
                    this.$http.get(this.hint.url.replace(/{param}/, this.hint.param)).then((response)=>{
                        this.handle(response);
                    })
                }
            },
            handle(response){
                this.options = response.data.options;
                this.choice = this.options.length>0?this.options[0].value:'';
                // this.$set('options', response.data.res['options']);
                // this.$set('choice', this.options.length>0?this.options[0].value:'');
            }
        }
    }
</script>
<style>
    
</style>