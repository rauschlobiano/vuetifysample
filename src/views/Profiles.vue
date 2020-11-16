<template>
<v-app>
    <v-row>
        <v-col class="ml-4">
            <div class="text-h5">Profiles Management</div>
        </v-col>
        <v-col>
            <v-progress-circular v-if="loading" indeterminate color="primary"></v-progress-circular>
        </v-col>
    </v-row>

    <v-row>
        <v-col class="ml-4 mr-4">
            <v-data-table :height="700" :dense="true" :headers="profileHeader" :items="profiles" item-key="profid" :items-per-page="20" class="elevation-4" v-model="selected" :single-select="true">
                <template slot="item" slot-scope="props">
                    <tr @click="showDialog(props.item)">
                        <td>{{ props.item.profid }}</td>
                        <td>{{ props.item.accountname }}</td>
                        <td>{{ props.item.address }}</td>
                        <td>{{ props.item.gender.genderdescrip }}</td>
                        <td>{{ props.item.proftype.proftypedescrip }}</td>
                        <td>{{ props.item.remarks }}</td>
                    </tr>
                </template>
            </v-data-table>
        </v-col>
    </v-row>
    <v-layout row justify-center>
        <v-dialog v-model="dialog" persistent max-width="600px" absolute>

            <v-card>
                <v-card-title>
                    <h5><small>Profile ID:</small> {{ selected.profid }}</h5>
                    <br>
                </v-card-title>
                <v-card-text>
                    <v-container grid-list-md>
                        <v-layout wrap>

                            <v-flex xs12>
                                <v-text-field label="Account Name*" required v-model="selected.accountname"></v-text-field>
                            </v-flex>

                            <v-flex xs12>
                                <v-text-field label="Address" hint="Full Address" v-model="selected.address"></v-text-field>
                            </v-flex>

                            <v-flex xs6>
                                <v-select :items="genders" v-model="selected.gender" item-value="genderid" item-text="genderdescrip"></v-select>
                            </v-flex>

                        </v-layout>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" @click="dialog = false">Close</v-btn>
                    <v-btn color="blue darken-1" @click="dialog = false">Save</v-btn>
                </v-card-actions>
            </v-card>

        </v-dialog>
    </v-layout>

</v-app>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import axios from "axios";

export default {
    name: "Home",
    components: {
        //HelloWorld
    },
    computed: {
        console: () => console,
        window: () => window,

    },
    watch: {

    },
    methods: {
        clickedRow: (item, row) => {
            row.select(true);
            console.log(item);
        },
        doubleClicked: () => {
            this.dialog = true;
        },
        showDialog(a) {

            this.selected.profid = a.profid;
            this.selected.accountname = a.accountname;
            this.selected.address = a.address;
            this.selected.gender = a.gender;
            this.selected.proftype = a.proftype;
            this.selected.remarks = a.remarks;

            this.dialog = true;

        },

    },
    mounted() {
        this.loading = true;

        axios
            .get("http://localhost:8000/api/profiles")
            .then((response) => (this.profiles = response.data))
            .catch(function (error) {
                console.log(error);
            })
            .then(function () {
                console.log('done loading profiles');
            });
        axios
            .get("http://localhost:8000/api/genders")
            .then((response) => {
                this.genders = response.data;
                //console.log(this.genders)
            })
            .catch(function (error) {
                console.log(error);
            })
            .then(function () {
                console.log('done loading genders');
            });
        axios
            .get("http://localhost:8000/api/proftypes")
            .then((response) => (this.proftypes = response.data))
            .catch(function (error) {
                console.log(error);
            })
            .then(function () {
                console.log('done loading proftypes');
            });

        this.loading = false;
    },
    data() {
        return {
            name: "",
            loading: true,
            dialog: false,
            gendersArray: [],
            profiles: [],
            genders: [],
            proftypes: [],
            selected: [],
            profileHeader: [{
                    text: "Profile ID",
                    align: "start",
                    sortable: true,
                    value: "profid",
                },
                {
                    text: "Account Name",
                    align: "start",
                    sortable: true,
                    value: "accountname",
                },
                {
                    text: "Address",
                    align: "start",
                    sortable: true,
                    value: "address",
                },
                {
                    text: "Gender",
                    align: "start",
                    sortable: true,
                    value: "gender.genderdescrip",
                },
                {
                    text: "Type",
                    align: "start",
                    sortable: true,
                    value: "proftype.proftypedescrip",
                },
                {
                    text: "Notes",
                    align: "start",
                    sortable: true,
                    value: "remarks",
                },
            ],

        };
    },
};
</script>

<style>

.v-data-table>.v-data-table__wrapper>table>tbody>tr>td {
   font-size: 11px !important;
}
</style>
