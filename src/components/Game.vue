<template>
    <div class="game">
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHealth" max="1000"/>
            <div class="cast">
                <div v-if="isDevilCasting"></div>
            </div>
        </div>

        <div :class="jesusAnimation" class="jesus">
            <img src="../assets/jesus.jpeg">
            <progress :value="jesusHealth" max="1000"/>

            <div class="actions">
                <action name="Jesus smite" :cooldown="8" @use="smite" />
            </div>
        </div>
    </div>
</template>

<script>
import Action from './Action.vue'

export default {
    components: {
        Action,
    },
    data () {
        return {
            devilHealth: 1000,
            jesusHealth: 1000,
            jesusAnimation: '',
            isDevilCasting: false,
        }
    },
    mounted () {
        setInterval(() => {
            this.isDevilCasting = true
            setTimeout(() => {
                this.jesusHealth -= 100
                this.isDevilCasting = false
            }, 1000)
        }, 3000)
    },
    methods: {
        smite () {
            this.devilHealth -= 80
            this.jesusAnimation = 'smite'
            setTimeout(() => this.jesusAnimation = '', 250)
        }
    }
}
</script>

<style lang="less">
@import '../main';
</style>
