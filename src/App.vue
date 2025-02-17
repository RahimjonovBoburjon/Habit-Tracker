<template>
  <div class="min-h-screen bg-gradient-to-r from-blue-500 to-teal-500 flex flex-col items-center py-10 mb-8">
    <h1 class="text-4xl font-bold text-white mb-8">Habit Tracker</h1>
    <add-habit @addHabit="addHabit" />
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mt-8 w-full px-4">
      <habit-card v-for="habit in habits" :key="habit.id" :habit="habit" @updateHabit="updateHabit"
        @deleteHabit="deleteHabit" />
    </div>
  </div>

  <footer
    class="bg-gradient-to-r from-teal-400 to-blue-500 text-white text-lg py-4 fixed bottom-0 left-0 right-0 shadow-lg rounded-t-lg">
    <p class="font-semibold text-center">
      Powered by <span class="text-yellow-300"><a href="https://github.com/RahimjonovBoburjon">Bobur</a></span>
    </p>
  </footer>
</template>

<script>
import HabitCard from './components/HabitCard.vue'
import AddHabit from './components/AddHabit.vue'

export default {
  components: {
    HabitCard,
    AddHabit,
  },
  data() {
    return {
      habits: JSON.parse(localStorage.getItem('habits')) || [],
    }
  },
  methods: {
    addHabit(newHabit) {
      this.habits.push(newHabit)
      this.saveHabits()
    },
    updateHabit(updatedHabit) {
      const index = this.habits.findIndex(habit => habit.id === updatedHabit.id)
      if (index !== -1) {
        this.habits[index] = updatedHabit
        this.saveHabits()
      }
    },
    deleteHabit(habitId) {
      this.habits = this.habits.filter(habit => habit.id !== habitId)
      this.saveHabits()
    },
    saveHabits() {
      localStorage.setItem('habits', JSON.stringify(this.habits))
    },
  },
}
</script>

<style scoped>
footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 1rem;
  color: white;
  text-align: center;
  font-size: 1.125rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
  border-top-left-radius: 1rem;
  border-top-right-radius: 1rem;
}

footer p {
  margin: 0;
}

footer span {
  font-weight: bold;
  color: #e2fb24;
}
</style>