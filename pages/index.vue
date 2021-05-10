<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>  
        <v-container>
            <v-row justify="center">
                <h2 id="textHeading" class="my-12">View your personalized Spotify statistics</h2>
            </v-row>
        </v-container>
        <v-container>
            <v-row justify="center">
                <v-card id="most-played"
                    max-width="800"
                >
                    <v-img id="backgroundMusicImg" height="250"
                        src="https://www.incimages.com/uploaded_files/image/1920x1080/getty_506068552_298876.jpg"
                    ></v-img>
                    <v-btn @click="sendToSpotifyLogin()" x-large class="my-12" color="#1DB954" rounded>Login with Spotify</v-btn>
                </v-card>
            </v-row>
        </v-container>
    </v-app>
</template>

<script>
import AppBarAndDrawer from '../components/AppBarAndDrawer.vue'

export default {
    data: () => ({
    
    }),

    components: {
        AppBarAndDrawer
    },
    methods: {
        sendToSpotifyLogin() {
            var redirect_uri = ""
            if(window.webpackHotUpdate) {
                redirect_uri = "http://localhost:3000/oauthcallback"
            } else {
                redirect_uri = "https://sleepylionheart.dev/oauthcallback"
            }
            const url = `https://accounts.spotify.com/authorize?client_id=1313a38061744d86a9537ef2bd563767&redirect_uri=${redirect_uri}&response_type=token&state=123&scope=user-read-private%20user-read-email%20user-top-read`
            window.location.href = url
        }
    }
}
</script>

<style scoped>

    #most-played {
        margin: 50px;
        text-align: center;
    }

    #backgroundMusicImg {
        opacity: 0.8;
    }

    #textHeading {
        font-family: Cochin;
        font-size: 40px;
    }

</style>