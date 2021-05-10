<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>  
        <v-container>
            <h2>Dashboard Page</h2>
            <h3>Your email address: {{myProfileData.data.email}}</h3>
            <h3>Your total followers: {{myProfileData.data.followers.total}}</h3>
        </v-container>
        <v-container>
            <v-row justify="center">
                <v-btn @click="getMyTopSongs()" x-large class="my-12" color="#1DB954" max-width="300px" rounded>Get My Top Songs</v-btn>
            </v-row>
        </v-container>
        <v-row>
            <template v-for="item in myTopData.items">
                <v-col cols="3" :key="item.id">
                    <v-card class="my-12 mx-12">
                        <v-card-title>{{item.name}}</v-card-title>
                        <v-card-text v-for="artist in item.artists" :key="artist.id">{{artist.name}}</v-card-text>
                        <v-img
                            :src = item.album.images[0].url
                        ></v-img>
                        <v-list-item @click="playSong(item.external_urls.spotify)">
                            <v-list-item-icon>
                                <v-icon color="#1DB954">mdi-play</v-icon>
                            </v-list-item-icon>
                            <v-list-item-title>Play Song</v-list-item-title>
                        </v-list-item>                         
                    </v-card>
                </v-col>
            </template>
        </v-row>
    </v-app>
</template>


<script>
import AppBarAndDrawer from '../components/AppBarAndDrawer.vue'
import axios from 'axios'

export default {
    data: function() {
        return {
            myProfileData: {},
            token: "",
            myTopData: {}
        }
    },

    created() {
        this.myProfileData = this.$route.params.myData
        this.token = this.$route.params.token
    },

    methods: {
        async getMyTopSongs() {
            var url = 'https://api.spotify.com/v1/me/top/tracks?time_range=medium_term&limit=50&offset=5'
            let config = {
                headers: {
                    Authorization: `Bearer ${this.token}`,
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                },
            }
            const res = await axios.get(url, config).then(data => this.myTopData = data.data)
        },
        playSong(url) {
            window.open(url, "_blank")
        }
    },
    components: {
        AppBarAndDrawer
    }
}
</script>

<style scoped>

</style>