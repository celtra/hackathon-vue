<template>
    <div>
        <div class="devil">
            <img src="../assets/devil.svg">
            <progress :value="devilHealth" max="1000"/>
        </div>

        <div class="jesus">
            <img src="../assets/jesus.svg">
            <progress :value="jesusHealth" max="1000"/>
        </div>
    </div>
</template>

<script>
import Action from './Action.vue'

export default {
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
