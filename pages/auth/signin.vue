<template>
  <div class="d-flex align-center justify-center fill-height">
    <v-card width="400" elevation="10" class="pa-4">
      <div class="d-flex justify-center mb-4">
        <v-img src="/logo.png" height="50" width="50" contain></v-img>
      </div>

      <h2 class="text-center">Login Page</h2>
      <v-card-text>
        <v-form>
          <v-text-field
            v-model="username"
            outlined
            label="Username"
            type="text"
            prepend-inner-icon="mdi-account"
          ></v-text-field>

          <v-text-field
            v-model="password"
            outlined
            label="Password"
            type="password"
            prepend-inner-icon="mdi-lock"
          ></v-text-field>
        </v-form>
      </v-card-text>

      <v-card-actions class="pt-4">
        <v-btn color="primary" block large @click="handleLogin">Login</v-btn>
      </v-card-actions>

      <!-- Divider -->
      <div class="text-center my-4">
        <v-divider></v-divider>
        <span class="overline grey--text">OR</span>
        <v-divider></v-divider>
      </div>

      <!-- Google Sign-In Button -->
      <v-card-actions>
        <v-btn block color="white" class="google-btn" elevation="2" @click="signinWithGoogle">
          <v-icon left color="red darken-1">mdi-google</v-icon>
          Sign in with Google
        </v-btn>
      </v-card-actions>
    </v-card>

    
  </div>
</template>
  
<script>
export default {
  layout: "auth",
  methods:{
    signinWithGoogle(){
      this.$auth.loginWith('google')
    }
  },
  data() {
    return {
      username: "",
      password: "",
    };
  },
  
};
</script>