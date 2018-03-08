<template lang='pug'>
.vue-index
    .reactive-title {{ reactiveTitle() }}
    header.hero.is-primary
        div.hero-body
         div.container
          h1.title Analog Clock
          h2.subtitle made by vue

    section.main.section
        clock

    footer.footer
        div.container
            div.content.has-text-centerd
</template>

<script lang='ts'>
import { Vue, Component } from 'vue-property-decorator';
import VueUtil from '@/scripts/util/VueUtil';
import RootVue from '@/components/base/RootVue';
import Sample from '@/components/sample/Sample.vue';
import Clock from '@/components/part/Clock.vue';

import Buefy from 'buefy';

Vue.use(Buefy);

/**
 * Vue Component
 */
@Component
export default class Index extends RootVue {
    public title: string = 'AnalogClock';

    protected beforeCreate(): void {
        // Inner Vue 登録
        VueUtil.registerComponents([Clock]);
    }
}
</script>

<style lang='sass'>
@import 'all'
.vue-index


</style>
