<script setup>
 import { ref } from 'vue'
 import { useRouter } from "vue-router";
import {useAuth} from '../../services/auth'

const router = useRouter();
const { login, loading, error } = useAuth()
 

  const rules = {
    required: value => !!value || 'Required.',
    min: v => v.length >= 8 || 'Min 8 characters',
    emailMatch: () => (`The email and password you entered don't match`),
  }

  const show1 = ref(false)
  const show2 = ref(true)
  const password = ref(null)
  const userName = ref(null)

  async function handleLogin() {
  
  if (!userName.value || !password.value) {
    console.error('Email and password are required')
    return
  }
  
  try {
    await login({
      email: userName.value,
      password: password.value
    })
   
    // Redirect after successful login
    router.push('/homepage').then(() => {
        router.go(0); // Reloads the current route
    });
  } catch (err) {
    // Error is already handled by the auth service
    console.error('Login failed', err)
  }
}

</script>

<template>
    <v-container width="50%" class="text-center" mt="12" background-color:#CFD0D6>
        <v-row>
            <v-col md="12">
                <v-form>
                    <v-row>
                        <v-col md="12">
                            <v-icon color="#EC8856" icon="mdi-weight-lifter" size="large" class="mt-12"></v-icon>
                        </v-col>
                        <v-row>
                            <v-col>
                                <div class="text-display-small font-weight-medium">Welcome to MacFit Gym</div>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Username</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field v-model="userName"></v-text-field>
                            </v-col>
                        </v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Password</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field 
                                    v-model="password"
                                    :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                                    :rules="[rules.required, rules.min]"
                                    :type="show1 ? 'text' : 'password'"
                                    @click:append="show1 = !show1"
                                    variant="outlined"
                                ></v-text-field>
                            </v-col>
                    </v-row>
                    <v-row>
                        <v-col md="12">
                            <v-btn color="#EC8856" variant="elevated" @click="handleLogin">Log in</v-btn>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col md="12">
                            <div>New to MacFit Gym? 
                               <router-link to="/signup">Create an Account</router-link> 
                            </div>
                        </v-col>
                    </v-row>
                </v-form>
            </v-col>
        </v-row>
    </v-container>
</template>