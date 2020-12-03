<template>
<div>
    <div class="ui action big fluid input">
        <input 
            type="text" 
            placeholder="Search Term..." 
            v-model="inputText" 
            @keydown.13.prevent="onInput(inputText)">
        <button class="ui orange button" @click="onInput(inputText)">Search Youtube-Videos!</button>
    </div>
</div>  
</template>

<script>
export default {
    name: 'SearchBar',
    data() {
        return { 
            inputText: ''
        }
    },
    methods: {
        onInput(term){
            this.$emit('termChange', term);
        }
    }
}
</script>
