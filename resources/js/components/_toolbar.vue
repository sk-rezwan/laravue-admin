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
      <v-menu offset-y>        
        <v-btn flat slot="activator" color="grey">
        <v-icon left>expand_more</v-icon>
        <span>User Management</span> 
        </v-btn>
        <v-list-tile to="/admin/users">
        <v-list-tile-action>
          <v-icon>account_circle</v-icon>
        </v-list-tile-action>
        <v-list-tile-content>
          <v-list-tile-title>Users</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>

      <v-list-tile to="/admin/roles">
        <v-list-tile-action>
          <v-icon>account_circle</v-icon>
        </v-list-tile-action>
        <v-list-tile-content>
          <v-list-tile-title>Role</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>

      <v-list-tile to="/admin/permissions">
        <v-list-tile-action>
          <v-icon>account_circle</v-icon>
        </v-list-tile-action>
        <v-list-tile-content>
          <v-list-tile-title>Permission</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>

      </v-menu>
      </v-toolbar-items>

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
    // props: ["user"],

  // data(){
  //     return {
  //       drawer: false,
  //       items: [
  //       { title: 'User' },
  //       { title: 'Role' },
  //       { title: 'Permission'}
  //     ]
  //   }
  // },



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