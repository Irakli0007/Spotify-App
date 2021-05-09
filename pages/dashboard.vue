<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>  
        <h2>Dashboard Page</h2>
        <h3>your email: {{myData.data.email}}</h3>
        <h3>your total followers: {{myData.data.followers.total}}</h3>
        <v-btn @click="getAlbum()">Get Album</v-btn>
    </v-app>
</template>


<script>
import AppBarAndDrawer from '../components/AppBarAndDrawer.vue'
import axios from 'axios'

export default {
    data: function() {
        return {
            myData: { },
            token: ""
        }
    },

    created() {
        this.myData = this.$route.params.myData
        this.token = this.$route.params.token
        console.log(this.token)
    },

    methods: {
        async getAlbum() {
            var url = 'https://api.spotify.com/v1/me/top/tracks?time_range=medium_term&limit=10&offset=5'
            let config = {
                headers: {
                    Authorization: `Bearer ${this.thisToken}`,
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                },
            }
            const res = await axios.get(url, config).then(data => console.log(data))
        }
    },
    components: {
        AppBarAndDrawer
    }
}
</script>

<style scoped>

</style>