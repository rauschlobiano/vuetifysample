<template>
<v-app style="-webkit-app-region: drag">
    <Navbar />

    <v-content>
        <router-view>
        </router-view>
    </v-content>
</v-app>
</template>

<script>
import Navbar from '@/components/Navbar.vue';

export default {
    name: 'App',

    components: {
        Navbar,
    },

    props: {
        source: String,
    },

    data: () => ({

    }),
};
</script>
