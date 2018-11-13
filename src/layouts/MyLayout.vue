<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-header>
     <q-toolbar color="secondary">
      <q-btn
        flat round dense
        icon="menu"
        @click="left = !left"
        aria-label="Toggle menu on left side"
      />
      <q-toolbar-title>
        Blogs
      </q-toolbar-title>
      <q-btn flat dense>SignUp / Login</q-btn>
    </q-toolbar>
     <q-layout-drawer
      side="left"
      v-model="left"
      :content-class="$q.theme === 'mat' ? 'bg-grey-3' : null"
    >
      <q-scroll-area class="fit">
        <q-list-header>
          <q-icon name="person" size="80pt" class="justify-center"/>
         </q-list-header>
        <q-item to="/" exact>
          <q-item-side icon="home" />
          <q-item-main label= 'Feed' />
        </q-item>
        <q-item to="/create">
          <q-item-side icon="chrome_reader_mode" />
          <q-item-main label= 'Create a new post' />
        </q-item>
        <q-item to="/login">
          <q-item-side icon="power_settings_new" />
          <q-item-main label= 'logout' />
        </q-item>
      </q-scroll-area>
    </q-layout-drawer>
    </q-layout-header>
    <q-page-container>
      <router-view />
      <q-dialog prevent-close
        v-model="customDialog"
      >
        <!-- <span slot="title" class="row">
          <div class="col-11"></div>
          <div class="col-1"><q-btn flat>X</q-btn></div>
        </span> -->
        <div slot="body" class="modalbody">
              <q-btn
                class="q-mb-lg q-ml-xl q-mt-lg"
                color="grey"
                text-color="black"
                label="Sign In With Google"
                style="width: 50%"
              />
              <q-btn
                color="grey"
                class="q-ml-xl"
                text-color="black"
                label="Sign In With facebook"
                style="width: 50%"
              />
        </div>
        <!-- <div slot="buttons" slot-scope="props" class="justify-center">
          <q-btn color="black" label="Cancel" @click="cancel(props.cancel)" />
        </div> -->
      </q-dialog>
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'MyLayout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      left: false,
      customDialog: true
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
.modal-body, .modal-scroll {
  overflow: hidden !important;
  max-height: 100%
}
.modal.minimized .modal-content {
  max-height: 100%;
  background-color:#f5f5f5;
}
</style>
