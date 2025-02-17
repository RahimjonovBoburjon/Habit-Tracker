<template>
    <div class="min-h-screen bg-gradient-to-r from-blue-500 to-teal-500 flex flex-col items-center py-10">
        <h1 class="text-4xl font-bold text-white mb-8">Habit Tracker</h1>

        <!-- Filter Buttons -->
        <div class="flex justify-center space-x-4 mt-6">
            <button @click="filterHabits('done')" class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600">
                Done
            </button>
            <button @click="filterHabits('notDone')"
                class="bg-gray-500 text-white px-4 py-2 rounded-lg hover:bg-gray-600">
                Not Done
            </button>
        </div>

        <!-- Add Habit Button -->
        <button @click="showAddHabitForm"
            class="bg-green-500 text-white px-4 py-2 rounded-full shadow-md hover:bg-green-600 flex items-center space-x-2 mt-6">
            <span>Add Habit</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" stroke="currentColor"
                viewBox="0 0 24 24" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 5v14m7-7H5"></path>
            </svg>
        </button>

        <!-- Habit List -->
        <div v-if="habits.length === 0" class="text-center text-gray-500 mt-8">
            <p>No habits yet! Start adding some habits.</p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mt-8 w-full px-4 overflow-y-auto max-h-screen">
            <habit-card v-for="habit in filteredHabits" :key="habit.id" :habit="habit" @updateHabit="updateHabit"
                @deleteHabit="deleteHabit" />
        </div>

        <!-- Habit Count -->
        <p class="text-lg font-semibold text-gray-800 mt-4">
            You have {{ habits.length }} habits to track!
        </p>
    </div>
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
            filteredHabits: [],
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
        filterHabits(status) {
            if (status === 'done') {
                this.filteredHabits = this.habits.filter(habit => habit.progress === 100);
            } else if (status === 'notDone') {
                this.filteredHabits = this.habits.filter(habit => habit.progress !== 100);
            } else {
                this.filteredHabits = this.habits;
            }
        },
        showAddHabitForm() {
        }
    },
    created() {
        this.filteredHabits = this.habits;
    }
}
</script>

<style scoped>
</style>