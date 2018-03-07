<template lang='pug'>

.vue-clock

    .hero.is-primary
        div.hero-body
         div.container
          h1.title Analog Clock
          h2.subtitle made by vue

    .date
        .columns.is-centered.has-text-centered.is-mobile
                .column.is-narrow: p {{ date.getMonth() + 1 }}
                .column.is-narrow: p 月
                .column.is-narrow: p {{ date.getDate() }}
                .column.is-narrow: p 日


    .clockarea
        img.clock-back(:src='imgs["clock-back"]')
        .hand#hour-hand: div(ref='hours') {{ updateHours() }}
        .hand#minute-hand: div(ref='minutes') {{ updateMinutes() }}
        .hand#second-hand: div(ref='seconds') {{ updateMilliseconds() }}
        .center: div

    .degital
        .columns.is-centered.has-text-centered.is-mobile
            .column.is-narrow: p {{ date.getHours() }}
            .column.is-narrow: p :
            .column.is-narrow: p {{ date.getMinutes() }}
            .column.is-narrow: p :
            .column.is-narrow: p {{ date.getSeconds() }}

    .footer
        div.container
            div.content.has-text-centerd


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
        const elem = this.$refs.seconds as HTMLElement;
        const deg = (360 * milliSeconds) / 60000;
        this.setRotate(elem, deg)
    }

    protected updateMinutes(): void {
        const minutes = this.date.getMinutes();
        const elem = this.$refs.minutes as HTMLElement;
        //$ref 子コンポーネント参照する
        const deg = (360 * minutes) / 60;
        this.setRotate(elem , deg)
    }

    protected updateHours(): void {
        const hours = this.date.getHours()
        + this.date.getHours();
        const elem = this.$refs.hours as HTMLElement;
        const deg = (360 * hours) / 24;
        this.setRotate(elem , deg)
    }

}
</script>

<style lang='sass' scoped>
@import 'all'

html
    min-height: 100%

.clockarea
    height: 479px
    margin: 40px auto
    max-width: 479px
    position: relative

    .clock-back
        position: absolute
        width: 100%
        height: 100%

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

        &#minute-hand
            & > div
                background-color: black
                width: 4px

        &#hour-hand
            & > div
                background-color: black
                width: 8px
                height: 30%

        &#second-hand
            & > div
                background-color: red

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
            border-radius: 50%

</style>
