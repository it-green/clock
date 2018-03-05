<template lang='pug'>
.vue-clock
    .hand#hour-hand
    .hand#minutes-hand
    .hand#seconds-hand(ref='seconds')

</template>

<script lang='ts'>
import { Vue, Component } from 'vue-property-decorator';
import VueUtil from '@/scripts/util/VueUtil';

/**
 * Vue Component
 */
@Component
export default class Clock extends Vue {
     protected mounted(): void {
        this.setRotate(this.$refs.seconds as HTMLElement);
    }

    protected setRotate(div: HTMLElement): void {
        div.style.transform = 'rotate(40deg)';
    }
}
</script>

<style lang='sass' scoped>
@import 'all'
.vue-clock
    height: 700px
    margin: 40px auto
    max-width: 700px
    position: relative

    #seconds-hand
        background-color: gray
        margin: auto
        height: 100%
        width: 0.2%
</style>
