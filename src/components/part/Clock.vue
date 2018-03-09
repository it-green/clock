<template lang='pug'>
.vue-clock

    .date
        .columns.is-centered.has-text-centered.is-mobile
            .column.is-narrow: p {{ date.getMonth() + 1 }}
            .column.is-narrow: p 月
            .column.is-narrow: p {{ date.getDate() }}
            .column.is-narrow: p 日


    .clockarea
        img.clock-back(:src='imgs["clock-back"]')
        .hand#hoursHand: div(ref='hours') {{ updateHours() }}
        .hand#minutesHand: div(ref='minutes') {{ updateMinutes() }}
        .hand#secondsHand: div(ref='seconds') {{ updateMilliseconds() }}
        .center: div

    .degital
        .columns.is-centered.has-text-centered.is-mobile
            .column.is-narrow: p {{ date.getHours() }}
            .column.is-narrow: p :
            .column.is-narrow: p {{ date.getMinutes().toString().padStart(2, '0') }}
            .column.is-narrow: p :
            .column.is-narrow: p {{ date.getSeconds().toString().padStart(2, '0') }}
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
    protected imgs: Imgs = {
        'clock-back': require('@/resources/img/clock.jpg')
    }
    private date: Date = new Date();

    protected mounted(): void {
        setInterval(() => {
            this.date = new Date();
        }, 30);
    console.log(this.date);
    }

    protected setRotate(elem: HTMLElement, deg: number) {          //要素の指示　 deg=角度つまり、角度を数字で表すように指示
        if (elem == null) {
            return;
        }

        elem.style.transform = `translate(-50%, -100%) rotate(${deg}deg)`;
    }

    protected updateMilliseconds(): void {
        const milliSeconds = this.date.getSeconds() * 1000
            + this.date.getMilliseconds();
        // $ref 子コンポーネント参照する
        const elem = this.$refs.seconds as HTMLElement;
        const deg = (360 * milliSeconds) / 60000;
        this.setRotate(elem, deg)
    }

    protected calcSecondsPerMinit(): number {
        return (this.date.getSeconds() * 1000 + this.date.getMilliseconds()) / 60000;
    }

    protected calcMinutesPerHour(): number {
        return (this.date.getMinutes() + this.calcSecondsPerMinit()) / 60;
    }

    protected updateMinutes(): void {
        const minutes = this.date.getMinutes() + this.calcSecondsPerMinit();
        const elem = this.$refs.minutes as HTMLElement;
        const deg = (360 * minutes) / 60;
        this.setRotate(elem , deg)
    }

    protected updateHours(): void {
        const hours = this.date.getHours() + this.calcMinutesPerHour();
        const elem = this.$refs.hours as HTMLElement;
        const deg = (360 * hours) / 12;
        this.setRotate(elem , deg)
    }

}
</script>

<style lang='sass' scoped>
@import 'all'

.vue-clock
    .date
        p
            font-size: 4em
            font-family: Batang
            color: black

    .degital
        p
            font-size: 4em
            font-family: Batang
            color: black

    .clockarea
        position: relative
        width: 100%
        max-width: 600px
        margin: 40px auto

        &::before
            content: ''
            display: block
            padding-top: 100%

        .clock-back
            position: absolute
            width: 100%
            height: 100%
            top: 0
            left: 0

        .hand
            position: absolute
            height: 90%
            width: 90%
            top: 50%
            left: 50%
            transform: translate(-50%, -50%)

            & > div
                background-color: gray
                position: absolute
                width: 2px
                height: 50%
                top: 50%
                left: 50%
                transform: translate(-50%, -100%)
                transform-origin: center bottom

            &#hoursHand
                & > div
                    background-color: black
                    width: 8px
                    height: 30%

            &#minutesHand
                & > div
                    background-color: black
                    width: 4px

            &#secondsHand
                & > div
                    background-color: red

        .center
            position: absolute
            height: 100%
            width: 100%
            top: 0
            left: 0
            border-radius: 50%

            & > div
                background-color: black
                position: absolute
                width: 30px
                height: 30px
                top: 50%
                left: 50%
                transform: translate(-50%, -50%)
                border-radius: 50%

    @media screen and (max-width: $tablet)
        font-size: 2.4vw

</style>
