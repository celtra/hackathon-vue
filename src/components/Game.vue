<template>
    <div>
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHealth" max="1000"/>
        </div>

        <div class="jesus">
            <img src="../assets/jesus.svg">
            <progress :value="jesusHealth" max="1000"/>

            <div class="actions">
                <ability name="Jesus headbutt" :cooldown="8" />
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
        }
    }
}
</script>

<style lang="less">
@import '../main';
</style>
