<template>
<v-navigation-drawer v-model="drawer" dark app class="grey darken-3 py-0">
    <v-container>
        <v-card class="mx-auto" max-width="434" tile>
            <v-img height="100%" src="https://cdn.vuetifyjs.com/images/cards/server-room.jpg">
                <v-row align="end" class="fill-height">
                    <v-col align-self="start" class="pa-0" cols="12">
                        <v-avatar class="profile" color="grey" size="164" tile>
                            <v-img src="https://cdn.vuetifyjs.com/images/profiles/marcus.jpg"></v-img>
                        </v-avatar>
                    </v-col>
                    <v-col class="py-0">
                        <v-list-item color="rgba(0, 0, 0, .4)" dark>
                            <v-list-item-content>
                                <v-list-item-title class="title">
                                    Ron Jones
                                </v-list-item-title>
                                <v-list-item-subtitle>Full Only but no Stack</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                </v-row>
            </v-img>
        </v-card>
    </v-container>
    <v-list nav>
        <v-list-item router to="/">
            <v-list-item-action>
                <v-icon small>fas fa-tachometer-alt</v-icon>
            </v-list-item-action>
            <v-list-item-content>
                <v-list-item-title>
                    <div class="text-h6">
                        Dashboard
                    </div>
                </v-list-item-title>
            </v-list-item-content>
        </v-list-item>

        <v-list-item router to="/profiles">
            <v-list-item-action>
                <v-icon small>fas fa-users</v-icon>
            </v-list-item-action>
            <v-list-item-content>
                <v-list-item-title>
                    Profiles
                </v-list-item-title>
            </v-list-item-content>
        </v-list-item>
    </v-list>
</v-navigation-drawer>
</template>

<script>
export default {
    data() {
        return {
            drawer: true,

        }
    },
}
</script>
