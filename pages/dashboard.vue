<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer> 
        <v-container>
            <v-row justify="center"> 
                <v-alert
                    border="top"
                    color="error"
                    dense
                    class="mt-2"
                    type="error"
                    :value="alert"
                    max-width="500px"
                >
                    Please select a time range.
                </v-alert>
            </v-row>
        </v-container>
        <v-container>
            <h2>Dashboard Page</h2>
            <h3>Your email address: {{myProfileData.data.email}}</h3>
            <h3>Your total followers: {{myProfileData.data.followers.total}}</h3>
        </v-container>
        <v-container>     
            <v-row justify="center">
                <v-card width="250px">
                   <v-col>
                        <v-btn @click="getMyTopSongs()" x-large class="my-12" color="#1DB954" rounded>Get My Top Songs</v-btn>
                    </v-col>
                    <v-col>
                        <v-select
                            @input="setSelection"
                            :items="selectItems"
                            label="Time Range"
                            outlined
                            item-color="#1DB954"
                        ></v-select>
                    </v-col>
                </v-card>
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
            myTopData: {},
            selectItems: ['short_term', 'medium_term', 'long_term'],
            selectedInterval : "",
            alert: false
        }
    },

    created() {
        this.myProfileData = this.$route.params.myData
        this.token = this.$route.params.token
    },

    methods: {
        async getMyTopSongs() {
            if(this.selectedInterval == "") {
                return this.createError();
            }
            var url = `https://api.spotify.com/v1/me/top/tracks?time_range=${this.selectedInterval}&limit=50&offset=5`
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
        },
        setSelection(value) {
            this.selectedInterval = value
            if(this.selectedInterval != "") {
                this.alert = false
            }
        },
        createError() {
            this.alert = true
        }

    },
    components: {
        AppBarAndDrawer
    }
}
</script>

<style scoped>



</style>