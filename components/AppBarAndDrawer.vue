<template>
    <div>
        <v-app-bar id="app-bar-text" color=#1DB954 dense > 
            <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
        </v-app-bar>
        <v-navigation-drawer
            v-model="drawer"
            absolute
            temporary    
        >
            <v-list
                nav
                dense
            >
                <v-list-item-group
                    v-model="group"
                >
                    <v-list-item @click="goToHomePage()">
                        <v-list-item-icon>
                        <v-icon>mdi-home</v-icon>
                        </v-list-item-icon>
                        <v-list-item-title>Home</v-list-item-title>
                    </v-list-item>

                    <v-list-item @click="goToMusicPage()">
                        <v-list-item-icon>
                        <v-icon>mdi-music</v-icon>
                        </v-list-item-icon>
                        <v-list-item-title>Music</v-list-item-title>
                    </v-list-item>

                    <v-list-item @click="goToStatsPage()">
                        <v-list-item-icon>
                        <v-icon>mdi-account</v-icon>
                        </v-list-item-icon>
                        <v-list-item-title>Stats</v-list-item-title>
                    </v-list-item>
                </v-list-item-group>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script>
export default {
    data: () => ({
        drawer: false,
        group: null,
    }),

    methods: {
        goToHomePage() {
            this.$router.push('/');
        },
        goToMusicPage() {
            this.$router.push('/music');
        },
        goToStatsPage() {
            this.$router.push('/stats');
        },
    }

}
</script>