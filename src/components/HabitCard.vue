<template>
    <div
        class="bg-white p-6 rounded-xl shadow-xl hover:shadow-2xl transform hover:scale-105 transition-all duration-200 relative">
        <button @click="deleteHabit"
            class="absolute top-2 right-2 bg-red-500 text-white p-1 px-3 rounded-full hover:bg-red-600 transition duration-200">
            <span class="text-xl">&times;</span>
        </button>

        <h3 class="text-xl font-semibold text-gray-800 mb-3 break-words">
            {{ habit.name }}
        </h3>

        <div class="relative w-full bg-gray-200 rounded-full h-4 mb-4">
            <div :style="{ width: habit.progress + '%' }" class="bg-green-500 h-4 rounded-full"></div>
            <span class="absolute inset-0 flex items-center justify-center text-sm font-semibold text-gray-800">
                {{ habit.progress }}%
            </span>
        </div>

        <div class="flex justify-between items-end mt-auto">
            <button @click="increaseProgress"
                class="bg-green-500 text-white px-4 py-2 rounded-lg hover:bg-green-600 transition duration-200">
                Mark as Done
            </button>
            <button @click="decreaseProgress"
                class="bg-red-500 text-white px-4 py-2 rounded-lg hover:bg-red-600 transition duration-200">
                Undo
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        habit: {
            type: Object,
            required: true
        }
    },
    methods: {
        increaseProgress() {
            if (this.habit.progress < 100) {
                this.habit.progress += 10
                this.$emit('updateHabit', this.habit)
            }
        },
        decreaseProgress() {
            if (this.habit.progress > 0) {
                this.habit.progress -= 10
                this.$emit('updateHabit', this.habit)
            }
        },
        deleteHabit() {
            this.$emit('deleteHabit', this.habit.id)
        }
    }
}
</script>

<style scoped></style>