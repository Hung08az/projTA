<template>
  <q-layout view="hHh lpR fFf" class="bg-grey-1">
    <q-header elevated class="bg-white text-grey-8" height-hint="64">
      <q-toolbar class="GNL__toolbar">
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          aria-label="Menu"
          icon="menu"
          class="q-mr-sm"
        />

        <q-toolbar-title v-if="$q.screen.gt.xs" shrink class="row items-center no-wrap">
          <img src="https://cdn.quasar.dev/img/layout-gallery/logo-google.svg">
          <span class="q-ml-sm">Takumi Match</span>
        </q-toolbar-title>

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn v-if="$q.screen.gt.sm" round dense flat color="text-grey-7" icon="apps">
            <q-tooltip>Google Apps</q-tooltip>
          </q-btn>
          <q-btn round dense flat color="grey-8" icon="notifications">
            <q-badge color="red" text-color="white" floating>
              2
            </q-badge>
            <q-tooltip>Notifications</q-tooltip>
          </q-btn>
          <q-btn round flat>
            <q-avatar size="26px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png">
            </q-avatar>
            <q-tooltip>Account</q-tooltip>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-white"
      :width="280"
    >
      <q-scroll-area class="fit">
        <q-list padding class="text-grey-8">
          <q-item class="GNL__drawer-item" v-ripple v-for="link in links1" :key="link.text" clickable>
            <q-item-section avatar>
              <q-icon :name="link.icon" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator inset class="q-my-sm" />

          <q-item class="GNL__drawer-item" v-ripple v-for="link in links2" :key="link.text" clickable>
            <q-item-section avatar>
              <q-icon :name="link.icon" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator inset class="q-my-sm" />

          <q-item class="GNL__drawer-item" v-ripple v-for="link in links3" :key="link.text" clickable>
            <q-item-section>
              <q-item-label>{{ link.text }} <q-icon v-if="link.icon" :name="link.icon" /></q-item-label>
            </q-item-section>
          </q-item>

          <div class="q-mt-md">
            <div class="flex flex-center q-gutter-xs">
              <a class="GNL__drawer-footer-link" href="javascript:void(0)" aria-label="Privacy">Privacy</a>
              <span> ?? </span>
              <a class="GNL__drawer-footer-link" href="javascript:void(0)" aria-label="Terms">Terms</a>
              <span> ?? </span>
              <a class="GNL__drawer-footer-link" href="javascript:void(0)" aria-label="About">About Google</a>
            </div>
          </div>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <q-page class="tw-flex">
        <q-scroll-area class="tw-grow"
          :thumb-style="thumbStyle"
          :bar-style="barStyle"
          visible="false"
        >
          <router-view />
        </q-scroll-area>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue';
import { fasEarthAmericas, fasFlask } from '@quasar/extras/fontawesome-v6';

const leftDrawerOpen = ref(false);
const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value;
};

const thumbStyle = {
  right: '4px',
  borderRadius: '5px',
  backgroundColor: '#027be3',
  width: '5px',
  opacity: 0.75,
};

const barStyle = {
  right: '2px',
  borderRadius: '9px',
  backgroundColor: '#027be3',
  width: '9px',
  opacity: 0.2,
};

const links1 = [
  { icon: 'web', text: 'Top stories' },
  { icon: 'person', text: 'For you' },
  { icon: 'star_border', text: 'Favourites' },
  { icon: 'search', text: 'Saved searches' },
];
const links2 = [
  { icon: 'flag', text: 'Canada' },
  { icon: fasEarthAmericas, text: 'World' },
  { icon: 'place', text: 'Local' },
  { icon: 'domain', text: 'Business' },
  { icon: 'memory', text: 'Technology' },
  { icon: 'local_movies', text: 'Entertainment' },
  { icon: 'directions_bike', text: 'Sports' },
  { icon: fasFlask, text: 'Science' },
  { icon: 'fitness_center', text: 'Health ' },
];
const links3 = [
  { icon: '', text: 'Language & region' },
  { icon: '', text: 'Settings' },
  { icon: 'open_in_new', text: 'Get the Android app' },
  { icon: 'open_in_new', text: 'Get the iOS app' },
  { icon: '', text: 'Send feedback' },
  { icon: 'open_in_new', text: 'Help' },
];
</script>

<style lang="sass">
.GNL
  &__toolbar
    height: 64px
  &__toolbar-input
    width: 55%
  &__drawer-item
    line-height: 24px
    border-radius: 0 24px 24px 0
    margin-right: 12px
    .q-item__section--avatar
      .q-icon
        color: #5f6368
    .q-item__label
      color: #3c4043
      letter-spacing: .01785714em
      font-size: .875rem
      font-weight: 500
      line-height: 1.25rem
  &__drawer-footer-link
    color: inherit
    text-decoration: none
    font-weight: 500
    font-size: .75rem
    &:hover
      color: #000
</style>
