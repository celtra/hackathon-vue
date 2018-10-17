<template>
    <div class="game">
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHealth" max="1000"/>
        </div>

        <div class="jesus">
            <img :class="jesusAnimation" src="../assets/jesus.jpeg">
            <progress :value="jesusHealth" max="1000"/>

            <div class="actions">
                <action name="Jesus headbutt" :cooldown="8" @use="headbutt" />
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
        }
    },
    methods: {
        headbutt () {
            this.devilHealth -= 80
            this.jesusAnimation = 'jesus-headbutt'
            setTimeout(() => this.jesusAnimation = '', 250)
        }
    }
}
</script>

<style lang="less">
@import '../main';
</style>
