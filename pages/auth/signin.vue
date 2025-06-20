<template>
    <div class="d-flex align-center justify-center fill-height">
      <v-card width="400" elevation="10" class="pa-4">
        <v-img
        src="/logo.png"
        height="50"
        width="50"
        >
        </v-img>
        <h2 class="text-center ">Sign In</h2>
        <v-card-text>
          <v-form>
            <v-text-field
              outlined
              label="Username"
              type="text"
              prepend-inner-icon="mdi-account"
            ></v-text-field>
            <v-text-field
              outlined
              label="Password"
              type="password"
              prepend-inner-icon="mdi-lock"
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions class="pt-4">
          <v-btn color="primary" block large>Sign In</v-btn>
        </v-card-actions>
      </v-card>
    </div>
  </template>
  
<script>
export default {
    layout: "auth"
}
</script>