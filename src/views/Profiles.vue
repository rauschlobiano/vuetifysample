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
                    <tr @click="showAlert(props.item)">
                        <td>{{ props.item.profid }}</td>
                        <td>{{ props.item.accountname }}</td>
                        <td>{{ props.item.address }}</td>
                        <td>{{ props.item.gender.genderdescrip }}</td>
                        <td>{{ props.item.proftype.proftypedescrip }}</td>
                        <td>
                            <v-btn slot="activator" small fab color="info" @click="dialog=true">
                                <v-icon>edit</v-icon>
                            </v-btn>
                        </td>
                    </tr>
                </template>
            </v-data-table>
        </v-col>
    </v-row>
    <v-layout row justify-center>
        <v-dialog v-model="dialog" persistent max-width="600px" absolute>

            <v-card>
                <v-card-title>
                    <h5>{{ selected.profid }} - {{ selected.accountname }}</h5>
                    <br>
                </v-card-title>
                <v-card-text>
                    <v-container grid-list-md>
                        <v-layout wrap>

                            <v-flex>
                                <v-text-field label="Account Name*" required></v-text-field>
                            </v-flex>

                            <v-flex>
                                <v-text-field label="Legal middle name" hint="example of helper text only on focus"></v-text-field>
                            </v-flex>

                            <v-flex>
                                <v-text-field label="Legal last name*" hint="example of persistent helper text" persistent-hint required></v-text-field>
                            </v-flex>

                            <v-flex xs12 sm6>
                                <v-autocomplete :items="selected.genders" label="Gender" multiple></v-autocomplete>
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
        dialog(val) {
            if (val) {
                document.addEventListener('mousedown', this.mousedownHandler)
            } else {
                document.removeEventListener('mousedown', this.mousedownHandler)
            }
        }
    },
    methods: {
        clickedRow: (item, row) => {
            row.select(true);
            console.log(item);
        },
        doubleClicked: (row) => {
            console.log(row);
        },
        showAlert(a) {
            console.log(this.selected);

            this.selected.profid = a.profid;
            this.selected.accountname = a.accountname;
            this.selected.gender = a.gender;
            this.selected.proftype = a.proftype;
            this.selected.genders = [];

            //to convert object to array
            for (let gen in a.gender) {
                this.selected.genders.push(gen);
            }
        }
    },
    mounted() {
        this.loading = true;
        axios
            .get("http://localhost:8000/api/profiles")
            .then((response) => (this.profiles = response.data));
        this.loading = false;
    },
    data() {
        return {
            name: "",
            loading: true,
            dialog: false,
            profiles: [],
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
            ],

        };
    },
};
</script>

<style>
.v-data-table>.v-data-table__wrapper>table>tbody>tr>td {
    font-size: 10px;
}
</style>
