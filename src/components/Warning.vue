<template>
<div class="ui icon red large message" v-show="isMessage">
    <i class="bullhorn icon"></i>
    <div class="content">
        <div class="header">
        SORRY! The request cannot be completed because you have exceeded the quota.
        </div>
        <p>Try again tomorrow!</p>
    </div>
</div>
</template>

<script>
export default {
    name: 'Warning',
    props: ['isMessage']
}
</script>