<template>
    <div class="action" @click="use">
        <p>{{ name }}</p>
        <div v-if="!isAvailable">{{ Math.ceil(remainingCooldown) }}</div>
    </div>
</template>

<script>
export default {
    props: {
        name: String,
        cooldown: Number,
    },
    data () {
        return {
            remainingCooldown: 0,
        }
    },
    computed: {
        isAvailable () {
            return this.remainingCooldown <= 0
        }
    },
    mounted () {
        setInterval(() => {
            this.remainingCooldown -= 50 / 1000
        }, 50)
    },
    methods: {
        use () {
            if (this.isAvailable) {
                this.remainingCooldown = this.cooldown
                this.$emit('use')
            }
        }
    }
}
</script>