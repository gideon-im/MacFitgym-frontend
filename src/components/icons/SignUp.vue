<script setup>
 import { ref } from 'vue'

  const rules = {
    required: value => !!value || 'Required.',
    min: v => v.length >= 8 || 'Min 8 characters',
    passwordMatch: () => password === confirmPassword || 'Passwords must match',
    emailMatch: () => (`The email and password you entered don't match`),
  }

  const show1 = ref(false)
  const show2 = ref(true)
  const password = ref(null) //Password Model

  const confirmPassword = ref(null)
  const show1confirm = ref(false)

  //Models
  const firstName =ref(null)
  const lastName =ref(null)
  const email =ref(null)
  const phoneNumber =ref(null)
  const gender =ref(null)
  const dob =ref(null)
  const gymLocation =ref(null)

  function signUp(){
    //create user object

    const userDetails= {
        name: firstName.value + lastName.value,
        email: email.value,
        phone: phoneNumber.value,
        dob: dob.value,
        gender: gender.value,
        gymLocation: gymLocation.value,
        password: password.value
    }

    //store this data

    try{
        localStorage.setItem('userDetails', JSON.stringify(userDetails))
    }catch (err){
        console.error("Sign up process failed")
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
                            <v-img src="MacFitLogo.png"></v-img>
                        </v-col>
                        <v-row>
                            <v-col>
                                <div class="text-display-small font-weight-medium">Welcome to MacFit Gym</div>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">First name</div>
                            </v-col> 
                            <v-col md="6">
                                <v-text-field variant="outlined" v-model="firstName"></v-text-field>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Last name</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field variant="outlined" v-model="lastName"></v-text-field>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Email</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field variant="outlined" v-model="email"></v-text-field>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Phone Number</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field type="number" variant="outlined" v-model="phoneNumber"></v-text-field>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Gender</div>
                            </v-col>
                            <v-col md="6">
                                <v-radio-group inline>
                                    <v-radio label="Male" value="one"></v-radio>
                                    <v-radio label="Female" value="two"></v-radio>
                                </v-radio-group>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Date Of Birth</div>
                            </v-col>
                            <v-col md="6">
                                
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Gym Locations</div>
                            </v-col>
                            <v-col md="6">
                               <v-select
                                    label="Select"
                                    :items="['CBD', 'Madaraka', 'Westlands', 'Buruburu']"
                                    variant="outlined"
                                    v-model="gymLocation"
                                ></v-select>
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
                            <v-col md="6">
                                <div class="text-display-large font-weight-medium text-right">Confirm Password</div>
                            </v-col>
                            <v-col md="6">
                                <v-text-field 
                                    v-model="confirmPassword"
                                    :append-icon="show1confirm ? 'mdi-eye' : 'mdi-eye-off'"
                                    :rules="[rules.required, rules.min, rules.passwordMatch]"
                                    :type="show1 ? 'text' : 'password'"
                                    @click:append="show1 = !show1"
                                    variant="outlined"
                                ></v-text-field>
                            </v-col>
                    </v-row>
                    <v-row>
                        <v-col md="12">
                            <v-btn color="#EC8856" variant="elevated" @click="signUp">Sign up</v-btn>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col md="12">
                            <div>Already have an account?
                                <router-link to="/login">Back to Login</router-link>
                            </div>
                        </v-col>
                    </v-row>
                </v-form>
            </v-col>
        </v-row>
    </v-container>
</template>