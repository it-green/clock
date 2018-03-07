<template lang='pug'>
.vue-clock
    .hand#hour-hand: div(ref='hours') {{ updateHours() }}
    .hand#minute-hand: div(ref='minutes') {{ updateMinutes() }}
    .hand#second-hand: div(ref='seconds') {{ updateMilliseconds() }}
    .center: div


</template>

<script lang='ts'>
import { Vue, Component } from 'vue-property-decorator';
import VueUtil from '@/scripts/util/VueUtil';
import { setInterval } from 'timers';

/**
 * Vue Component
 */
@Component
export default class Clock extends Vue {
    private date: Date = new Date();

    protected mounted(): void {
        setInterval(() => {
            this.date = new Date();
        }, 30);
    }

    protected setRotate(elem: HTMLElement, deg: number) {          //要素の指示　 deg=角度つまり、角度を数字で表すように指示
        if (elem == null) {
            return;
        }

        elem.style.transform = `rotate(${deg}deg)`;
    }

    protected updateMilliseconds(): void {
        const milliSeconds = this.date.getSeconds() * 1000
            + this.date.getMilliseconds();
        const elem = this.$refs.seconds as HTMLElement;
        const deg = (360 * milliSeconds) / 60000;
        this.setRotate(elem, deg)
    }

    protected updateMinutes(): void {
        const minutes = this.date.getMinutes() * 1000
        + this.date.getMinutes();
        const elem = this.$refs.minutes as HTMLElement;
        //$ref 子コンポーネント参照できる
        const deg = (360 * minutes) / 60000;
        this.setRotate(elem , deg)
    }

    protected updateHours(): void{
        const hours = this.date.getHours() * 1000
        + this.date.getHours();
        const elem = this.$refs.hours as HTMLElement;
        const deg = (360 * hours) / 60000;
        this.setRotate(elem , deg)
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
                background-color: yellow
                width: 4px

    .center
        position: absolute
        height: 100%
        width: 100%
        border-radius: 50%

        & > div
            background-color: black
            position: absolute
            width: 30px
            height: 30px
            top: 50%
            left: 50%
            transform: translate(-50%, -50%)



</style>
