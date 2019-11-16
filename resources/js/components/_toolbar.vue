<template>
  <div>
    <v-toolbar>
      <v-toolbar-title>Title</v-toolbar-title>

      <v-spacer></v-spacer>

      <!-- navigation starts here-->
        <v-toolbar-items>
          <v-list-tile exact to="/admin">
            <v-icon>dashboard</v-icon>
                Dashboard
        </v-list-tile>
        

        <v-list-tile to="/admin/activities">
          <v-icon>settings</v-icon>
            <v-list-tile-title>Activities</v-list-tile-title>
        </v-list-tile>
      

        <v-list-tile to="/admin/settings">
          <v-icon>settings</v-icon>
            <v-list-tile-title>Settings</v-list-tile-title>
        </v-list-tile>

      </v-toolbar-items>

     <!--navigation ends here-->
      <!-- <template v-if="$vuetify.breakpoint.smAndUp">
        <v-btn icon>
          <v-icon>mdi-export-variant</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-delete-circle</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-plus-circle</v-icon>
        </v-btn>
      </template> -->

      <!-- dropdown -->
      <div class="text-center">
    <v-menu offset-y>
      <template v-slot:activator="{ on }">
        <v-btn
          color="primary"
          dark
          v-on="on"
        >
          User Management
        </v-btn>
      </template>
      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
          @click=""
        >
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
      <v-spacer></v-spacer>
      <v-spacer></v-spacer>
      
      <!--logout-->
      <v-menu offset-y origin="center center" :nudge-bottom="10" transition="scale-transition">
        <v-btn icon large flat slot="activator">
          <v-avatar size="30px">
            <img src="https://via.placeholder.com/150" alt="admin">
          </v-avatar>
        </v-btn>
        <v-list class="pa-0">
          <v-list-tile ripple="ripple" rel="noopener">
            <v-list-tile-content>
              <v-list-tile-title>{{user.name}}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>

        <v-list class="pa-0">
          <v-list-tile @click="logout" ripple="ripple" rel="noopener">
            <v-list-tile-action>
              <v-icon>account_circle</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>Logout</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
    </v-menu>

    </v-toolbar>
  </div>
</template>


<script>
export default {
  props: ["user"],

  data: () => ({
      items: [
        { title: 'Users', route: '/admin/users' },
        { title: 'Role', route: '/admin/roles' },
        { title: 'Permission', route: '/admin/permissions' },
      ],
    }),



  // data: () => ({
  //   drawer: null,
  //   allNotifications: [],
  //   unreadNotifications: [],
  // }),
  
  props: ["user"],
  // watch:{
  //     allNotifications(val){
  //         this.unreadNotifications =  this.allNotifications.filter(notification => {
  //           return notification.read_at == null;
  //       });
  //     }
  // },

  methods: {
    logout() {
      axios.post("/logout").then(response => window.location.reload());
    },
    // markAsRead() {
    //   axios.get("/mark-all-read/" + this.user.id).then(response=>{
    //       this.unreadNotifications = [];
    //   });
    // }
  },
 
  // created() {
  //   this.allNotifications = this.user.notifications;

  //   this.unreadNotifications =  this.allNotifications.filter(notification => {
  //       return notification.read_at == null;
  //     });

  //   Echo.private("App.User." + this.user.id).notification(notification => {
  //     this.allNotifications.unshift(notification.notification);
  //   });
  // }
};
</script>