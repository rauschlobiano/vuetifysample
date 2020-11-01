<template>
<v-app style="-webkit-app-region: drag">
    <Navbar />

    <v-main>
        <router-view>
        </router-view>
    </v-main>
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
