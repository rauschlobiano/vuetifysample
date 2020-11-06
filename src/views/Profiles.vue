<template>
<v-app>
    <v-row>
        <v-col class="ml-4">
            <div class="text-h5">Profiles Management</div>
        </v-col>
        <v-col>
        <v-progress-circular v-if="loading"
            indeterminate
            color="primary"
        ></v-progress-circular>
 
                <v-dialog
                v-model="dialog"
                persistent
                max-width="600px"
                >
                <template v-slot:activator="{ on, attrs }">
                    <v-btn
                    color="primary"
                    dark
                    v-bind="attrs"
                    v-on="on"
                    >
                    Open Dialog
                    </v-btn>
                </template>
                <v-card>
                    <v-card-title>
                    <span class="headline">Profile Details</span>
                    </v-card-title>
                    <v-card-text>
                    <v-container>
                        <v-row>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field label="Legal first name*" required></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field label="Legal middle name" hint="example of helper text only on focus"></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field label="Legal last name*" hint="example of persistent helper text" persistent-hint
                            required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12"> <v-text-field label="Email*" required ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Password*"  type="password"
                            required
                            ></v-text-field>
                        </v-col>
                        <v-col
                            cols="12"
                            sm="6"
                        >
                            <v-select
                            :items="['0-17', '18-29', '30-54', '54+']"
                            label="Age*"
                            required
                            ></v-select>
                        </v-col>
                        <v-col
                            cols="12"
                            sm="6"
                        >
                            <v-autocomplete
                            :items="['Skiing', 'Ice hockey', 'Soccer', 'Basketball', 'Hockey', 'Reading', 'Writing', 'Coding', 'Basejump']"
                            label="Interests"
                            multiple
                            ></v-autocomplete>
                        </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                    </v-card-text>
                    <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                        color="blue darken-1"
                        text
                        @click="dialog = false"
                    >
                        Close
                    </v-btn>
                    <v-btn
                        color="blue darken-1"
                        text
                        @click="dialog = false"
                    >
                        Save
                    </v-btn>
                    </v-card-actions>
                </v-card>
                </v-dialog>
            
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
            this.currentRow = e;
        },
       

    },
    mounted() {
        this.loading = true;
          axios
            .get('http://localhost:8000/api/profiles')
            .then(response => (this.profiles = response.data))
            this.loading = false;
    },
    data() {
        return {
            loading: true,
            dialog: false,
            currentRow: [],
            profileHeader: [
                {text: 'Profile ID', align: 'start', sortable: true, value: 'profid'},
                {text: 'Account Name', align: 'start', sortable: true, value: 'accountname'},
                {text: 'Address', align: 'start', sortable: true, value: 'address'},
                {text: 'Gender', align: 'start', sortable: true, value: 'gender.genderdescrip'},
                {text: 'Type', align: 'start', sortable: true, value: 'proftype.proftypedescrip'},
            ],
            profiles: [],
        }
    },
}
</script>

<style>
.v-data-table>.v-data-table__wrapper>table>tbody>tr>td 
{
  font-size: 10px;
}
</style>
