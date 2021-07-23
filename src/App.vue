<template>
  <div id="app">
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">
          <img alt="Assettte logo" src="./assets/logo.png" />
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/admin">Admin</router-link>
            <router-link class="nav-link" to="/settings">Settings</router-link>
          </b-navbar-nav>

          <b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown right>
              <template #button-content>
                <img alt="profile picture" src="./assets/profile.jpg" class="profile-picture" />
                <span class="downArrow">&#x2228;</span>
              </template>
              <b-dropdown-item href="#">Profile</b-dropdown-item>
              <b-dropdown-item href="#">Sign Out</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import './assets/scss/variables';

.bg-info {
  background: #010D2F !important;
  padding: 0px 16px;
}
.profile-picture {
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.dropdown-toggle::after {
  display: none;
}
.navbar-collapse.collapse {
  @media screen and (min-width: 500px) {
    margin-left: 200PX;
  }
}
.nav-link {
  padding: 20px 15px !important;
}
.nav-link.router-link-exact-active.router-link-active {
  color: $linkColor;
  border-bottom: 3px solid;
}
.downArrow {
  color: #000;
}
</style>
