<template>
  <v-app>
    <v-system-bar window lights-out height="20"></v-system-bar>
      <v-app-bar app color="white" flat>
        <v-app-bar-nav-icon class="ml-10" @click.stop="draw = !draw" v-if="!draw"/>
        <v-toolbar-title v-if="!draw">Cooperation</v-toolbar-title>
      </v-app-bar>
    <v-navigation-drawer
      v-model="draw"
      app
    >
    <v-list-item>
      <v-list-item-avatar size="40px" color="grey"></v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>Cooperation</v-list-item-title>
          <v-list-item-subtitle v-if="!user">웹 사이트 버전</v-list-item-subtitle>
          <v-list-item-subtitle v-else>사용자 등급</v-list-item-subtitle>
        </v-list-item-content>
      <v-list-item-action>
        <v-btn icon @click.stop="draw = false">
          <v-icon size="16px" light>mdi-close</v-icon>
        </v-btn>
      </v-list-item-action>
    </v-list-item>
    <v-divider />
    <v-list>
      <v-list-group
        v-for="item in list"
        :key="item.title"
        :prepend-icon="item.action"
      >
        <template v-slot:activator>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item-content>
        </template>
      </v-list-group>
    </v-list>
    </v-navigation-drawer>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Default extends Vue {
  draw = false
  user = true
  userName = '정지민'
  list = [
    {
      action: 'mdi-school',
      items: [{ title: 'List Item' }],
      title: 'Education'
    },
    {
      action: 'mdi-run',
      items: [{ title: 'List Item' }],
      title: 'Family'
    },
    {
      action: 'mdi-bottle-tonic-plus',
      items: [{ title: 'List Item' }],
      title: 'Health'
    },
    {
      action: 'mdi-content-cut',
      items: [{ title: 'List Item' }],
      title: 'Office'
    },
    {
      action: 'mdi-tag',
      items: [{ title: 'List Item' }],
      title: 'Promotions'
    }
  ]
}
</script>

<style scoped>
  .b {
    font-size: 15px;
    color: grey;
  }
</style>
