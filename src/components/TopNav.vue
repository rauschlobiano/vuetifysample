<template>
  <div>
    <v-app-bar src="https://picsum.photos/1920/1080?random" dark>
    <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

    <v-icon large dark>widgets</v-icon>     
    <v-toolbar-title>JPFL2020</v-toolbar-title>

    <v-spacer></v-spacer>
   
      <v-btn class="mx-2" color="white" outlined router to="/">
        <v-icon dark small>fa-home</v-icon>
         Home
      </v-btn>
      <v-btn class="mx-2" color="white" outlined router to="/profiles">
        <v-icon dark small>fa-users</v-icon>
         Profiles
      </v-btn>

    <v-spacer></v-spacer>
    </v-app-bar>
  </div>
</template>
<script>
export default {
    data() {
        return {
            links: [],
        }
    },
}
</script>