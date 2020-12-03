<template>
<div class="ui three stackable cards">
    <VideoListItem 
        v-for="video in videos" 
        :video="video" 
        :key="video.etag">
        {{video}}
    </VideoListItem>
</div>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
    name: 'VideoList',
    components: {
        VideoListItem
    },
    props: ['videos']
}
</script>

<style scoped>

</style>