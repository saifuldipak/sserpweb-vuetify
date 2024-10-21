<template>
  <v-responsive>
    <v-app>
      <v-app-bar elevation="3">
        <v-btn icon="mdi-menu" @click="drawer = !drawer"></v-btn>
        <v-app-bar-title class="text-h5">Client Database</v-app-bar-title>
      </v-app-bar>
      <v-navigation-drawer v-model="drawer">
        <v-list-item v-for="view in views" link @click="changeView(view)" :key="view.id" :prepend-icon="view.icon"
          :title="view.name"></v-list-item>
      </v-navigation-drawer>

      <v-main>
        <v-toolbar v-if="showToolbar">
          <v-btn :icon="viewIcon" size="large"></v-btn>
          <v-toolbar-title class="text-h6">{{ viewName }}</v-toolbar-title>
          <v-icon icon="mdi-plus" color="success" size="x-large"></v-icon>
          <v-icon icon="mdi-magnify" color="primary" size="x-large" @click="showSearch = !showSearch"></v-icon>
        </v-toolbar>
        <!-- <v-container class="w-50">
          <v-alert text="..." title="Warning" type="warning" icon="$warning" closable border></v-alert>

        </v-container> -->
        <v-form v-if="showSearch" @submit.prevent="searchItem">
          <v-container :class="width">
            <v-row>
              <v-text-field label="Client Name" hide-details="auto" clearable append-inner-icon="mdi-magnify"
                @click:append-inner="searchItem"></v-text-field>
            </v-row>
          </v-container>
        </v-form>
      </v-main>
    </v-app>
  </v-responsive>
</template>

<script setup>
import { computed } from 'vue';
import { useDisplay } from 'vuetify';

const showSearch = ref(false)
const showToolbar = ref(false)
const viewIcon = ref("")
const viewName = ref("")
const drawer = ref(false)
const views = ref([{ id: 1, name: "Clients", icon: "mdi-bank" },
{ id: 2, name: "Services", icon: "mdi-cloud" },
{ id: 3, name: "Pops", icon: "mdi-office-building-cog-outline" },
{ id: 4, name: "Service Providers", icon: "mdi-briefcase" },
])


const changeView = (view) => {
  viewName.value = view.name
  viewIcon.value = view.icon
  showToolbar.value = true
}

const searchItem = () => {
  console.log("search")
}

const { name } = useDisplay()

const width = computed(() => {
  switch (name.value) {
    case 'xs': return "w-100"
    case 'sm': return "w-75"
    case 'md': return "w-50"
    case 'lg': return "w-50"
    case 'xl': return "w-33"
    case 'xxl': return "w-25"
  }
  return undefined
})

</script>
