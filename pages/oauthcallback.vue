<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>   
        <h2>Callback Page</h2>
        <v-container>
            <v-row justify="center">
                <v-card
                    max-width="800"
                >
                    <v-img height="250"
                        src="https://www.incimages.com/uploaded_files/image/1920x1080/getty_506068552_298876.jpg"
                    ></v-img>
                    <v-btn @click="Login()" x-large class="my-12" color="#1DB954" rounded>Login</v-btn>
                </v-card>
            </v-row>
        </v-container>
    </v-app>
</template>


<script>
import AppBarAndDrawer from '../components/AppBarAndDrawer.vue'
import axios from 'axios'

export default {
    data: function() {
        return {
            thisToken: "",
        }
    },

    created: function() {
        var currentURL = window.location.href
        var token = currentURL.split("#access_token=").pop().split("&token_type=")[0]
        //todo if the current url contains ("error")....  https://developer.spotify.com/documentation/general/guides/authorization-guide/#implicit-grant-flow
        this.thisToken = token
    },
    methods: {
        async Login() {
            var url = 'https://api.spotify.com/v1/me'
            let config = {
                headers: {
                    Authorization: `Bearer ${this.thisToken}`,
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }
            var myData = { }
            const res = await axios.get(url, config).then(data => myData = data)
            this.$router.push({name: 'dashboard', params: { myData: myData, token: this.thisToken } })
        }
    },
    components: {
        AppBarAndDrawer
    },
}
</script>

<style scoped>

</style>