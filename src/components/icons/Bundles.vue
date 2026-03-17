<script setup>
import { ref } from 'vue'
 import {useRouter} from "vue-router";

 const router = useRouter();

 const showBundleDialog = ref(false)
 const isLoggedIn = localStorage.getItem("authToken")
 const selectedBundle = ref(null)
 const selectedPrice = ref(null)
 
 function showBundle(name, price){
    if (isLoggedIn){
        selectedBundle.value = name
        selectedPrice.value = price
        showBundleDialog.value = true //open pop-up
    }else{
        router.push('/login')
    }
 }

 function subscribe(){
     const userDetails = JSON.parse(localStorage.getItem('user'))
     userDetails.subscription = {
        name: selectedBundle.value,
        price: selectedPrice.value
     }
     localStorage.setItem('user', JSON.stringify(userDetails))
     showBundleDialog.value = false
 }
</script>

<template>
    <v-container style="background-color:#CFD0D6" class="mt=12">
        <v-row>
            <div class="text-display-medium mb=12">Bundles and Pricing</div>
        </v-row>
        <v-row>
            <div class="text-label-medium font-italic">Click on a bundle to subscribe</div>
        </v-row>
        <v-row>
            <v-col md="3">
                <v-card class="text-center"@click="showBundle('Daily', 500)">
                    <v-icon color="#EC8856" icon="mdi-calendar-today-outline" size="large" class="mt=8"></v-icon>
                    <v-card-title color="#EC8856">Daily</v-card-title>
                    <v-card-title>Ksh 500 </v-card-title>

                </v-card>
            </v-col>
            <v-col md="3"> 
                <v-card class="text-center" @click="showBundle('1 Month', 8000)">
                    <v-icon color="#EC8856" icon="mdi-calendar-month-outline" size="large" class="mt=8"></v-icon>
                    <v-card-title color="#EC8856">1 Month</v-card-title>
                    <v-card-title>Ksh 8000 </v-card-title>

                </v-card>
            </v-col>
            <v-col md="3"> 
                <v-card class="text-center" @click="showBundle('3 Months', 23000)">
                    <v-icon color="#EC8856" icon="mdi-clock-outline" size="large" class="mt=8"></v-icon>
                    <v-card-title color="#EC8856">3 Months</v-card-title>
                    <v-card-title>Ksh 23000</v-card-title>

                </v-card>
            </v-col>
            <v-col md="3"> 
                <v-card class="text-center" @click="showBundle('6 Months', 45000)">
                    <v-icon color="#EC8856" icon="mdi-clock-outline" size="large" class="mt=8"></v-icon>
                    <v-card-title color="#EC8856">6 Months</v-card-title>
                    <v-card-title>Ksh 45000</v-card-title>

                </v-card>
            </v-col>
            <v-col md="3"> 
                <v-card class="text-center" @click="showBundle('1 Year', 88000)">
                    <v-icon color="#EC8856" icon="mdi-timer-sand-full" size="large" class="mt=8"></v-icon>
                    <v-card-title color="#EC8856">1 year</v-card-title>
                    <v-card-title>Ksh 88000</v-card-title>

                </v-card>
            </v-col>
        </v-row>
        <v-row>
            <v-col md="12">

            </v-col>
        </v-row>

    </v-container>
    <!-- What's Included -->
     <v-container>
        <v-row>
            <v-col md="12">
                <div class="text-display-medium mb-12">What's included in your bundle</div>
            </v-col>
        </v-row>
        <v-row>
            <v-col md="3">
                <v-card class="test-center">
                    <v-icon color="#EC8856" icon="mdi-clock-outline" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">5.00am-9.00pm</v-card-title>
                </v-card>
            </v-col>
            <v-col md="3">
                <v-card>
                    <v-icon color="#EC8856" icon="mdi-dumbbell" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">Dedicated men's and women's zones</v-card-title>
                </v-card>
            </v-col>
            <v-col md="3">
                <v-card>
                    <v-icon color="#EC8856" icon="mdi-weight-lifter" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">Access to qualified trainers</v-card-title>
                </v-card>
            </v-col>
            <v-col md="3">
                <v-card>
                    <v-icon color="#EC8856" icon="mdi-food" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">Personalized nutrition guidance</v-card-title>
                </v-card>
            </v-col>
        </v-row>
        <v-row>
            <v-col md="3">
                <v-card>
                    <v-icon color="#EC8856" icon="mdi-parking" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">Free parking & locker</v-card-title>
                </v-card>
            </v-col>
            <v-col md="3">
                <v-card>
                    <v-icon color="#EC8856" icon="mdi-shower-head" size="large" class="mt-8"></v-icon>
                    <v-card-title color="#EC8856">Steam Room & showers</v-card-title>
                </v-card>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                 <div class="text-display-medium mt=8">How to Join</div>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <v-list>
                    <v-list-item>1.Select your preferred membership plan.</v-list-item>
                    <v-list-item>2.Visit us or fill out the online form.</v-list-item>
                    <v-list-item>3.Make a secure payment at the front desk.</v-list-item>
                    <v-list-item>4.Begin your fitness journey immediately!</v-list-item>
                </v-list>
            </v-col>
        </v-row>
     </v-container>
     <!--Dialog-->
     <v-dialog v-model="showBundleDialog" max-width="600" >

      <v-card prepend-icon="mdi-account" title="Subscribe to Bundle" >
        <v-card-text>
          You are about to subscribe to {{ selectedBundle }} at {{ selectedPrice }}. Click on the button below to complete payment
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
         <v-spacer></v-spacer>
          <v-btn text="Close" variant="plain" @click="showBundleDialog = false" ></v-btn>
          <v-btn color="primary" variant="tonal" @click="subscribe()" >Subscribe</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>