<template lang='pug'>
.vue-clock
    h1 これは、時計です
</template>

<script lang='ts'>
import { Vue, Component } from 'vue-property-decorator';
import VueUtil from '@/scripts/util/VueUtil';

/**
 * Vue Component
 */
@Component
export default class Clock extends Vue {
}
</script>

<style lang='sass' scoped>
@import 'all'

.vue-clock
</style>
