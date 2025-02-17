<template>
    <div
        class="bg-white p-6 rounded-xl shadow-xl max-w-sm mx-auto transform hover:scale-105 transition-all duration-200">
        <input v-model="habitName" type="text" placeholder="Enter habit name"
            class="w-full p-3 mb-4 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 transition duration-200" />
        <button @click="addHabit"
            class="w-full bg-blue-500 text-white p-3 rounded-lg shadow-md hover:bg-blue-600 transition duration-300 ease-in-out transform hover:scale-105">
            Add Habit
        </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            habitName: '',
        }
    },
    methods: {
        addHabit() {
            if (this.habitName.trim()) {
                const newHabit = {
                    id: Date.now(),
                    name: this.habitName,
                    progress: 0,
                }
                this.$emit('addHabit', newHabit)
                this.habitName = ''
            }
        },
    },
}
</script>

<style scoped></style>