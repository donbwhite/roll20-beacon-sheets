<template>
    <div class="col" style="display: flex; gap:10px">
        <select
            class="age-atk-select form-select"
            data-testid="test-spell-weaponType-input"
            placeholder="Spell Cost"
            v-model="mod.modifiedValue"
        >
            <option value="Bonus">Bonus</option>
            <option value="Penalty">Penalty</option>
        </select>
    </div>
    <div class="col">
        <!-- <input class="form-control" v-if="mod.modifiedValue === 'Variable'" type="number" placeholder="0" v-model="mod.variable" />
        <input class="form-control" v-if="mod.modifiedValue === 'Roll'" type="text" placeholder="1d6" v-model="mod.variable" /> -->
  
                        <input v-if="mod.modifiedValue === 'Bonus'" type="number"  class="form-control" placeholder="0" min="0" v-model="mod.bonus" @change="useModifiersStore().getDamageBonus()" />
                     
                        <input v-if="mod.modifiedValue === 'Penalty'" type="number"  class="form-control" placeholder="0" max="0"  v-model="mod.penalty" />
             
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { useModifiersStore } from '@/sheet/stores/modifiers/modifiersStore';
const props = defineProps({
    mod:{ type: Object}
})
const damageType = ref('');
</script>