<template>
<v-app style="-webkit-app-region: drag">
    <TopNav />
   

    <v-main>
        <router-view>
        </router-view>
    </v-main>
</v-app>
</template>

<script>
import TopNav from '@/components/TopNav.vue';
//import Navbar from '@/components/Navbar.vue';

export default {
    name: 'App',

    components: {
        //Navbar,
        TopNav,
    },

    props: {
        source: String,
    },

    data: () => ({

    }),
};
</script>
