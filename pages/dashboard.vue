<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>  
        <h2>Dashboard Page</h2>
        <h3>your email: {{myProfileData.data.email}}</h3>
        <h3>your total followers: {{myProfileData.data.followers.total}}</h3>
        <v-btn @click="getMyTopSongs()">Get Top Songs</v-btn>
        <ul>
            <li v-for="item in myTopData.items" :key="item.id">{{item.name}}</li>
        </ul>
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
        }
    },
    components: {
        AppBarAndDrawer
    }
}
</script>

<style scoped>

</style>