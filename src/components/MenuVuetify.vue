<template>
    <v-app>
        <v-app-bar app color="primary">
        <v-app-bar-nav-icon @click="toggleDrawer"></v-app-bar-nav-icon>
        <v-toolbar-title>Справочник разработчика</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
            <v-menu>
            <template v-slot:activator="{ props }">
              <v-btn v-bind="props">Админ</v-btn>
            </template>
              <v-list>
                <v-list-item to="/roles" link>Роли</v-list-item>
                <v-list-item to="/logs" link>Логи</v-list-item>
                <v-list-item to="/users" link>Пользователи</v-list-item>
              </v-list>
          </v-menu>
          <v-menu v-if="userName">
            <template v-slot:activator="{ props }">
              <v-btn v-bind="props">{{ userName }}</v-btn>
            </template>
            <v-list>
              <v-list-item @click="logout" link>Выйти</v-list-item>
            </v-list>
          </v-menu>
          <v-btn v-else to="/login" text>Вход</v-btn>
        </v-toolbar-items>
    </v-app-bar>
    <v-navigation-drawer v-model="drawerOpen" app>
      <v-list>
        <v-list-item to="/home" link >
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Главная</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
       </v-list>
    </v-navigation-drawer>
    <v-main class="container mt-4"> 
      <router-view></router-view>
    </v-main>
    </v-app>
  </template>
  
  <script>

  export default {
    data() {
      return {
        drawerOpen: false, // Изначально меню закрыто
        userName: null
      };
    },
    mounted() {
      this.userName = localStorage.user_name;
    },
    methods: {
      toggleDrawer() {
        this.drawerOpen = !this.drawerOpen; // Инвертируем текущее состояние меню
      },
      logout() {
        delete localStorage.access_token;
        delete localStorage.user_name;
        this.$router.push('/login');
      }
    },
  };

  </script>