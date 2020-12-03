<template>
<div class="orange card">
    <div class="image">
        <img :src="thimbnailUrl" data-lity="data-lity" :href="videoSrc">
    </div>
    <div class="textZone">
        <div>
            <span class="titleText" v-html="video.snippet.title"></span>
        </div>
        <div class="meta dateText">
            <span class="date">{{ this.momentDate(this.video.snippet.publishedAt) +" by " + this.video.snippet.channelTitle}}</span>
        </div>
        <div>
            <span class="descriptionText" v-html="video.snippet.description"></span>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'VideoListItem',
    props: ['video'],
    computed: {
        thimbnailUrl(){
            return this.video.snippet.thumbnails.medium.url;
        },
        videoSrc(){
            const { videoId } = this.video.id;
            return `https://www.youtube.com/embed/${videoId}`;
        }
    },
    methods: {
        momentDate(videoDate){
            var moment = require('moment'); 
            return moment(videoDate).format('YYYY/MM/DD');
        }
    }
}
</script>

<style scoped>
.card{
    font-family: "Gill Sans", sans-serif;
}
.textZone{
    padding: 10px;
}
.titleText {
    font-weight: 600;
    font-size: 1.3rem;
}
.dateText{
    margin: 3px 0 3px 0;
    text-align: right;
}
.descriptionText{
    font-size: 1.0rem;
}
</style>> 