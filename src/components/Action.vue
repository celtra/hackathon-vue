<template>
    <div class="action" @click="use">
        <div class="action__name">{{ name }}</div>
        <div v-if="!isAvailable" class="action__cooldown">{{ Math.ceil(remainingCooldown) }}</div>
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
            if (!this.isAvailable) {
                this.remainingCooldown -= 50 / 1000
            }
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

<style lang="less" scoped>

.action {
  width: 60px;
  height: 60px;
  border: 1px solid;
  padding: 10px 0;
  box-sizing: border-box;
  position: relative;
  border-radius: 3px;
  cursor: pointer;

  &__name {
    text-align: center;
  }

  &__cooldown {
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    line-height: 60px;
    text-align: center;
    font-size: 32px;
    background-color: rgba(255, 255, 255, 0.7);
    user-select: none;
    cursor: default;
  }
}
</style>
