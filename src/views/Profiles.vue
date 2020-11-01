<template>
<v-app>
    <v-row>
        <v-col class="ml-4">
            <div class="text-h5">Profiles Management</div>
        </v-col>
    </v-row>
    
    <v-row>
        <v-col class="ml-4 mr-4">
            <v-data-table 
            :height="700"
            :dense="true"
            :headers="profileHeader" 
            :items="profiles" 
            :items-per-page="20" 
            @click:row="clickedRow"
            class="elevation-1"></v-data-table>
        </v-col>
    </v-row>
    
</v-app>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios';

export default {
    name: 'Home',
    components: {
        //HelloWorld
    },
    computed: {
        console: () => console,
        window: () => window,
    },
    methods: {
        clickedRow: (e) => {
            console.log(e);
        }
    },
    mounted() {
          axios
            .get('http://localhost:8000/api/profiles')
            .then(response => (this.profiles = response.data))
    },
    data() {
        return {
            profileHeader: [
                {text: 'Profile ID', align: 'start', sortable: true, value: 'profid'},
                {text: 'Account Name', align: 'start', sortable: true, value: 'accountname'},
                {text: 'Address', align: 'start', sortable: true, value: 'address'},
                {text: 'Gender', align: 'start', sortable: true, value: 'gender.genderdescrip'},
                {text: 'Type', align: 'start', sortable: true, value: 'proftype.proftypedescrip'},
            ],
            profiles: [],
            headers: [{
                    text: 'Dessert (100g serving)',
                    align: 'start',
                    sortable: false,
                    value: 'name',
                },
                {
                    text: 'Calories',
                    value: 'calories'
                },
                {
                    text: 'Fat (g)',
                    value: 'fat'
                },
                {
                    text: 'Carbs (g)',
                    value: 'carbs'
                },
                {
                    text: 'Protein (g)',
                    value: 'protein'
                },
                {
                    text: 'Iron (%)',
                    value: 'iron'
                },
            ],
            desserts: [{
                    name: 'Frozen Yogurt',
                    calories: 159,
                    fat: 6.0,
                    carbs: 24,
                    protein: 4.0,
                    iron: '1%',
                },                
            ],

        }
    },
}
</script>

<style scoped>
.v-data-table td {
  font-size: 10px;
}
</style>
