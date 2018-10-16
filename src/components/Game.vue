<template>
    <div class="game">
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHP" max="1000"/>
        </div>

        <div class="jesus">
            <img src="../assets/jesus.jpeg">
            <progress :value="godHP" max="1000"/>
        </div>
    </div>
</template>

<script>
import Action from './Action.vue'

export default {
}
</script>

<style lang="less">
@import '../main';
</style>
