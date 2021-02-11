<template>
    <div>
        <MenuBar></MenuBar>
        <SearchBar id="mySearch" @termChange="onTermChange"></SearchBar>
        <div :class="{mylists: videos.length>0}"  v-if="videos.length>0" >
            <h2>Search Results " {{this.query}} "</h2>
            <h3>Click the video-image, to watch the video!</h3>
            <div class="ui grid container">
                <VideoList :videos="videos"></VideoList>
            </div>
            <Pagination id="myPage" @pagination="onPagination" :pToken="prevToken" :nToken="nextToken"></Pagination>
        </div>
        <Warning :isMessage="isMessage"></Warning>
        
    </div>
</template>

<script>
import axios from 'axios';
import MenuBar from './components/MenuBar';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import Pagination from  './components/Pagination';
import Warning from  './components/Warning';

const API_KEY = 'MY_KEY';

export default {
    name: 'App',
    components: {
        MenuBar,
        SearchBar,
        VideoList,
        Pagination,
        Warning
    },
    data() {
        return {
            videos: [],
            isMessage: false,
            disP: true,
            disN: true,
            query: '',
            nextToken: '',
            prevToken: '',
            baseParams: {
                key: API_KEY,
                type: 'video',
                part: 'snippet',
                maxResults: 12,
                order: 'viewCount'
            }
        };
    },
    methods: {
        onTermChange(searchTerm){
            this.query = searchTerm;
            axios
            .get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    ...this.baseParams,
                    q: this.query
                }
            })
            .then(response => {
                this.videos = response.data.items;
                this.nextToken = response.data.nextPageToken;
                this.prevToken = response.data.prevPageToken;
                this.isMessage = false;
            })
            .catch(err => {
                if(err.response.status === 403) this.isMessage = true;
            })
        },
        onPagination(npToken){
            let myToken = '';
            if(npToken === 'next' && this.nextToken !== undefined) myToken = this.nextToken;
            else if(npToken === 'prev' && this.prevToken !== undefined) myToken = this.prevToken;
            else return;

            axios
            .get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    ...this.baseParams,
                    q: this.query,
                    pageToken: myToken
                }
            }).then(response => {
                this.videos = response.data.items;
                this.nextToken = response.data.nextPageToken;
                this.prevToken = response.data.prevPageToken;
                this.isMessage = false;
            })
            .catch(err => {
                if(err.response.status === 403) this.isMessage = true;
            });
        }
    }
};
</script>

<style scoped>
#mySearch {
    margin-top: 100px;
    margin-left: auto;
    margin-right: auto;
    width: 70%;
}
#myPage{
    margin-left: 42%;
    margin-top: 50px;
}
.container{
    width: 100%;
    height: 100%;
    margin-top: 50px;
}
.mylists {
    width: 90%;
    margin-top: 50px;
    margin-bottom: 50px;
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    border: 1px solid rosybrown;
    border-radius: 10px;
}
.message{
    margin-top: 50px;
}
</style>