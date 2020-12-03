<template> 
<div class="ui pagination menu">
    <a class="item" @click="onPage('prev')" :class="{disabled: pToken === undefined}">
        Prev
    </a>
    <div class="disabled item">
        ...
    </div>
    <a class="item" @click="onPage('next')" :class="{disabled: nToken === undefined}">
        Next
    </a>
</div>
</template>

<script>
export default {
    name: 'Pagination',
    props: ['nToken', 'pToken'],
    methods: {
        onPage(npToken){
            this.$emit('pagination', npToken);
        }
    }
}
</script>