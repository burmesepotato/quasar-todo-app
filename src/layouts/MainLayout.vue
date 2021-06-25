<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="showDrawer = !showDrawer"
        />
      </q-toolbar>

      <div class="q-px-lg q-pt q-mb-md">
        <div class="text-h5 text-weight-bold">Todo</div>
        <div class="text-h5 text-weight-thin">{{ todayDate }}</div>
      </div>

      <q-img
        src="statics/constellations@1920.jpg"
        class="header-image absolute-top"
      />
    </q-header>

    <q-drawer v-model="showDrawer" show-if-above :width="250" :breakpoint="720">
      <q-scroll-area
        style="
          height: calc(100% - 130px);
          margin-top: 130px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="checklist" />
            </q-item-section>

            <q-item-section> Todo </q-item-section>
          </q-item>

          <q-item to="/help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="statics/constellations@1920.jpg"
        style="height: 130px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img
              src="https://assets.codepen.io/2951126/internal/avatars/users/default.png?fit=crop&format=auto&height=80&version=1598424250&width=80"
            />
          </q-avatar>
          <div class="text-weight-bold">Burmese Potato</div>
          <div>@BurmesePotato</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from "components/EssentialLink.vue";
import { date } from "quasar";

export default {
  name: "MainLayout",
  components: { EssentialLink },
  data() {
    return {
      showDrawer: false,
    };
  },
  computed: {
    todayDate() {
      let timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd, MMM D");
    },
  },
};
</script>

<style lang="scss" scoped>
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.4;
  filter: brightness(0.7);
}
</style>