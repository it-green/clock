<template lang='pug'>
.vue-clock
    .hand#hour-hand: div(ref='hours')
    .hand#minute-hand: div(ref='minutes')
    .hand#second-hand: div(ref='seconds')

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
        this.setRotate1(this.$refs.seconds as HTMLElement);
        this.setRotate2(this.$refs.minutes as HTMLElement);
        this.setRotate3(this.$refs.hours as HTMLElement);
    }

    protected setRotate1(div: HTMLElement): void {
        div.style.transform = 'rotate(0deg)';
    }

    protected setRotate2(div: HTMLElement): void {
        div.style.transform = 'rotate(45deg)';
    }

    protected setRotate3(div: HTMLElement): void {
        div.style.transform = 'rotate(90deg)';
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

    .hand
        position: absolute
        height: 100%
        width: 100%

        & > div
            background-color: gray
            position: absolute
            width: 2px
            height: 50%
            top: 0%
            left: 50%
            transform: translate(-50%, 0)
            transform-origin: center bottom

        &#minute-hand
            & > div
                background-color: black
                width: 4px
</style>
