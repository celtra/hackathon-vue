<template>
    <div>
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHealth" max="1000"/>
            <div class="cast">
                <div v-if="isDevilCasting"></div>
            </div>
        </div>

        <div class="jesus">
            <img :class="jesusAnimation" src="../assets/jesus.svg">
            <progress :value="jesusHealth" max="1000"/>

            <div class="actions">
                <ability name="Jesus headbutt" :cooldown="2" @use="headbutt" />
                <ability name="Hear my prayer" :cooldown="4" @use="pray" />
                <ability name="Jesus dodge" :cooldown="3" @use="dodge" />
            </div>
        </div>
    </div>
</template>

<script>
import Ability from './Ability.vue'

export default {
    components: {
        Ability,
    },
    data () {
        return {
            devilHealth: 1000,
            jesusHealth: 1000,
            jesusAnimation: '',
            isDevilCasting: false,
            isJesusDodging: false,
        }
    },
    mounted () {
        setInterval(() => {
            this.isDevilCasting = true
            setTimeout(() => {
                if (this.isDevilCasting) {
                    if (!this.isJesusDodging) {
                        this.jesusHealth -= 200
                    }
                    this.isDevilCasting = false
                }
            }, 1000)
        }, 2000)
    },
    methods: {
        headbutt () {
            this.devilHealth -= 80
            this.jesusAnimation = 'jesus-headbutt'
            setTimeout(() => this.jesusAnimation = '', 250)
        },
        pray () {
            this.isDevilCasting = false
            this.jesusAnimation = 'jesus-pray'
            setTimeout(() => this.jesusAnimation = '', 1000)
        },
        dodge () {
            this.isJesusDodging = true
            this.jesusAnimation = 'jesus-dodge'
            setTimeout(() => {
                this.jesusAnimation = ''
                this.isJesusDodging = false
            }, 800)
        },
    }
}
</script>

<style lang="less">
@import '../main';
</style>
