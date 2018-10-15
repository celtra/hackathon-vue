<template>
    <div class="game">
        <div class="devil">
            <img src="../assets/devil.jpg">
            <progress :value="devilHP" max="1000"/>
            <div v-if="isCasting" class="progress"></div>
            <div class="actions"></div>
        </div>

        <div class="god">
            <img :class="activeAnimation" src="../assets/god.jpeg">
            <progress :value="godHP" max="1000"/>
            <div class="actions">
                <action name="Jesus headbutt" :cooldown="2" @use="headbutt"/>
                <action name="Jesus dodge" :cooldown="4" @use="dodge"/>
                <action name="Hear my prayer" :cooldown="7" @use="prayer"/>
            </div>
        </div>
    </div>
</template>

<script>
import Action from './Action.vue'

export default {
    components: {
        Action
    },
    data () {
        return {
            godHP: 1000,
            devilHP: 1000,
            isCasting: false,
            isDodging: false,
            activeAnimation: ''
        }
    },
    mounted () {
        setInterval(() => {
            this.isCasting = true
            setTimeout(() => {
                if (this.isCasting) {
                    if (!this.isDodging) {
                        this.godHP -= 100
                    }
                    this.isCasting = false
                }
            }, 1000)
        }, 3000)
    },
    methods: {
        headbutt () {
            this.devilHP -= 80
            this.activeAnimation = 'jesus-headbutt'
            setTimeout(() => this.activeAnimation = '', 250)
        },
        dodge () {
            this.isDodging = true
            this.activeAnimation = 'jesus-dodge'
            setTimeout(() => {
                this.activeAnimation = ''
                this.isDodging = false
            }, 800)
        },
        prayer () {
            this.isCasting = false
            this.activeAnimation = 'jesus-pray'
            setTimeout(() => this.activeAnimation = '', 1000)
        },
    }
}
</script>

<style scoped lang="less">

.game {
  width: fit-content;
  margin: 40px auto 0; 
}

.god,
.devil {
  width: 200px;
  min-height: 100px;
  margin-top: 20px;
}

img {
  height: 200px;
  display: block;
  margin: auto;
}

progress {
  width: 100%;
}

.progress {
  height: 15px;
  width: 100%;
  border: 1px solid;
  border-radius: 3px;
  animation: cast 1s linear;
}

.actions {
  display: flex;
  justify-content: space-between;
}

@keyframes cast {
    from { width: 0%; }
    to { width: 100%; }
}

.jesus-dodge {
  animation: dodge 0.8s linear;
}

@keyframes dodge {
  10% { transform: translateX(-50px); }
  20% { transform: translateX(50px); }
  40% { transform: translateX(-120px) scale(1.5); }
}

.jesus-headbutt {
  animation: headbutt 0.25s linear;
}

@keyframes headbutt {
  20% { transform: translateY(40px); }
  60% { transform: translateY(-200px); }
}

.jesus-pray {
  animation: pray 1s linear, vibrate 0.1s infinite;
}

@keyframes pray {
  90% { transform: scale(1.5); }
  100% { transform: scale(1); }
}

// @keyframes vibrate {
//     50% { transform: translate(-5px); }
//     100% { transform: translate(5px); }
// }
</style>
