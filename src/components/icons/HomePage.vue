<script setup>
import { ref } from 'vue'

const userName = ref("Gideon")

const stats = ref({
  workouts: 4,
  calories: 3200,
  time: 6,
  streak: 5
})

const todaysWorkout = ref([
  { name: "Bench Press", sets: 4, reps: 10 },
  { name: "Squats", sets: 4, reps: 12 },
  { name: "Plank", sets: 3, reps: "60 sec" }
])

const classes = ref([
  { name: "Yoga", time: "6:00 PM" },
  { name: "HIIT", time: "7:30 PM" },
  { name: "Strength Training", time: "Tomorrow 8:00 AM" }
])
</script>


<template>
  <div class="dashboard">

    <!-- Welcome Section -->
    <section class="welcome">
      <h1>Welcome back, {{ userName }} 💪</h1>
      <p>Ready for today's workout?</p>
    </section>

    <!-- Stats Cards -->
    <section class="stats">
      <div class="card">
        <h3>Workouts This Week</h3>
        <p>{{ stats.workouts }}</p>
      </div>

      <div class="card">
        <h3>Calories Burned</h3>
        <p>{{ stats.calories }}</p>
      </div>

      <div class="card">
        <h3>Workout Time</h3>
        <p>{{ stats.time }} hrs</p>
      </div>

      <div class="card">
        <h3>Workout Streak</h3>
        <p>{{ stats.streak }} days</p>
      </div>
    </section>

    <!-- Today's Workout -->
    <section class="workout">
      <h2>Today's Workout</h2>

      <ul>
        <li v-for="exercise in todaysWorkout" :key="exercise.name">
          {{ exercise.name }} — {{ exercise.sets }} × {{ exercise.reps }}
        </li>
      </ul>

      <button class="start-btn">Start Workout</button>
    </section>

    <!-- Upcoming Classes -->
    <section class="classes">
      <h2>Upcoming Classes</h2>

      <div class="class-card" v-for="c in classes" :key="c.name">
        <h3>{{ c.name }}</h3>
        <p>{{ c.time }}</p>
        <button>Reserve Spot</button>
      </div>
    </section>

    <!-- Quick Actions -->
    <section class="actions">
      <button>Start Workout</button>
      <button>Book Class</button>
      <button>View Progress</button>
      <button>Nutrition Plan</button>
    </section>

  </div>
</template>



<style scoped>

.dashboard{
  padding:40px;
  font-family:Arial;
}

.welcome{
  margin-bottom:30px;
}

.stats{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:20px;
  margin-bottom:40px;
}

.card{
  background:#f3f3f3;
  padding:20px;
  border-radius:10px;
  text-align:center;
}

.workout{
  margin-bottom:40px;
}

.start-btn{
  margin-top:15px;
  padding:10px 20px;
  background:black;
  color:white;
  border:none;
  border-radius:5px;
}

.classes{
  margin-bottom:40px;
}

.class-card{
  background:#fafafa;
  padding:20px;
  margin-bottom:10px;
  border-radius:10px;
}

.actions{
  display:flex;
  gap:15px;
}

.actions button{
  padding:10px 15px;
  border:none;
  background:#222;
  color:white;
  border-radius:5px;
}

</style>