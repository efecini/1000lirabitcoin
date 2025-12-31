<script setup>
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';
import ColorPicker from 'primevue/colorpicker';

import { ref } from 'vue';

const color = ref();
const text = ref('');
</script>

<template>
  <div>
    <InputText v-model="text" /> <Button label="Save" />
    {{ text }}
    <ColorPicker v-model="color" />
  </div>
</template>
