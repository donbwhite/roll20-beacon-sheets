<template>
    <div class="age-splash-screen">
        <h1>Select your game's ruleset</h1>
        <div class="age-splash-rulesets" v-if="!selectedSystem">
            <button class="age-ruleset-btn" aria-label="Fantasy AGE Ruleset" @click="selectSystem('fage2e');$emit('close')">
                <img src="/src/assets/logos/fantasyage.png" alt="Fantasy AGE" role="presentation">
            </button>
            <button class="age-ruleset-btn" aria-label="Modern AGE Ruleset" @click="selectSystem('mage');$emit('close')">
                <img src="/src/assets/logos/modernage.png"  alt="Modern AGE" role="presentation">
            </button>
            <button class="age-ruleset-btn" aria-label="Blue Rose AGE Ruleset" @click="selectSystem('blue rose');$emit('close')">
                <img src="/src/assets/logos/bluerose.png" alt="Blue Rose AGE" role="presentation">
            </button>
            <button class="age-ruleset-btn" aria-label="Expanse AGE Ruleset" @click="selectSystem('expanse')">
                <img src="/src/assets/logos/expansewhite.png" alt="Expanse AGE" role="presentation">
            </button>
        </div>
        <div v-else class="age-character-type-select">
            <button class="age-character-type-btn"  aria-label="Character" @click="selectExpanseCharType('Character');$emit('close')">
                <img :src="'/src/assets/icons/sensuousness.svg'" />
                <span>Character</span>
            </button>
            <button class="age-character-type-btn" aria-label="Ship" @click="selectExpanseCharType('Ship');$emit('close')">
                <img :src="'/src/assets/icons/starfighter.svg'" />
                <span>Ship</span>
            </button>
        </div>
        <h6>*This can be changed later in your sheet settings</h6>  
    </div>
</template>
<script setup>
import { useBioStore } from '@/sheet/stores/bio/bioStore';
import { useSettingsStore } from '@/sheet/stores/settings/settingsStore';
import { productLineStyle } from '@/utility/productLineStyle';
import { ref } from 'vue';

const settings = useSettingsStore();
const bio = useBioStore();
const selectedSystem = ref('');

const selectSystem = (system) => {
    if(system !== 'expanse'){
        settings.gameSystem = system;
    }
    if(system === 'expanse'){
        selectedSystem.value = system;
    }
}

const selectExpanseCharType = (type) => {
    settings.useFortune = true;
    settings.gameSystem = 'expanse';
    bio.type = type;
}
</script>
<style scoped lang="scss">
.age-splash-screen {
    background-image: linear-gradient(
        45deg,
        hsl(0deg 0% 0%) 0%,
        hsl(344deg 0% 3%) 18%,
        hsl(344deg 0% 6%) 26%,
        hsl(344deg 0% 8%) 33%,
        hsl(344deg 0% 9%) 39%,
        hsl(344deg 0% 11%) 44%,
        hsl(344deg 0% 13%) 50%,
        hsl(344deg 0% 14%) 56%,
        hsl(344deg 0% 16%) 61%,
        hsl(344deg 0% 18%) 67%,
        hsl(344deg 0% 19%) 74%,
        hsl(344deg 0% 21%) 82%,
        hsl(0deg 0% 23%) 100%
        );
    font-family:'Graphik', Helvetica, Arial, serif;
    text-align:center;
    height:100vh;
    width:100vw;
    display: grid;
    align-items: center;
    color:#FFF;
    justify-content: center;
    & h1 {
        text-transform: uppercase;
        margin:0;
    }
    & .age-splash-rulesets {
        display: grid;
        max-width: 850px;
        gap: 25px;
        & .age-ruleset-btn {
            background: none;
            border:none;
            & img {
                width: 100%;
                filter: grayscale(80%);
                transition: filter 0.5s ease;
            }
        }
        & .age-ruleset-btn:hover {            
            & img {                
                filter: grayscale(0%);
            }
        }
    }
}
.age-character-type-select {
    display: flex;
    gap: 25px;
    justify-content: center;
    & .age-character-type-btn {
        background: none;
        border: 2px solid #FFF;
        color: #FFF;
        padding: 15px;
        font-size: 1.2rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 10px;
        width: 150px;
        border-radius: 10px;
        font-family: 'Venus Rising', sans-serif;
        cursor: pointer;
        & img {
            width: 100px;
            filter: invert(100%);
        }
        &:hover {
            background-color: rgba(255,255,255,0.1);
        }
    }
}
@media (min-width:601px){
    .age-splash-rulesets {
        grid-template-columns: repeat(2,1fr);
        padding:10px 25px;

    }
}
@media (max-width:600px){
    .age-splash-rulesets {
        grid-template-columns: 1fr;
        padding:10px 50px;
    }
}
</style>