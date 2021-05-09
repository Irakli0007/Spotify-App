<template>
    <v-app>
        <AppBarAndDrawer></AppBarAndDrawer>
        <div id="content">
            <v-col>
                <v-row>
                    <v-container>
                        <v-card id="most-played"
                            height="400px"
                            width="400px"
                        >       
                        Stats Page
                        </v-card>
                    </v-container>
                </v-row>
            </v-col>
        </div>
    </v-app>
</template>

<script>
    import AppBarAndDrawer from '../components/AppBarAndDrawer.vue'

    export default {


        components: {
            AppBarAndDrawer
        },
    }
</script>

<style scoped>
    #most-played {
        margin: 50px;
    }
    #content {
        text-align: center;
    }

</style>