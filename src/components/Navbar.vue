<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Ido&Tal Recipes</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <router-link id="routLink" :to="{ name: 'main' }" class="nav-link">Main</router-link>
      <router-link id="routLink" :to="{ name: 'search' }" class="nav-link">Search </router-link>
      <router-link id="routLink" :to="{ name: 'about' }" class="nav-link">About </router-link>

      <span v-if="$root.store.username" >
        Hello Guest:
        <div style="display:inline-block">
            <router-link id="routLink" :to="{ name: 'register' }" class="nav-link" style="display:inline-block">Register </router-link>
            <router-link id="routLink" :to="{ name: 'login' }" class="nav-link" style="display:inline-block">Login </router-link>
        </div>
      </span>
      <span v-else style="display:inline">
        {{ $root.store.username }}: 
        <div style="display:inline">
            <div style="display:inline">
                <button @click="Logout" class="btn btn-outline-success my-2 my-sm-0">Logout </button>
            </div>
            <div class="dropdown" style="display:inline">
              <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Dropdown button
              </button>
              <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                <router-link class="dropdown-item" href="#">Action</router-link>
                <router-link class="dropdown-item" href="#">Another action</router-link>
                <router-link class="dropdown-item" href="#">Something else here</router-link>
              </div>
            </div>
            <!-- <li class="nav-item dropdown" style="display:inline-block">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Dropdown
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                <a class="dropdown-item" href="#">Action</a>
                <a class="dropdown-item" href="#">Another action</a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#">Something else here</a>
                </div>
            </li> -->
            <div style="display:inline-block">
                <router-link id="routLink" :to="{ name: 'login' }" class="nav-link" style="display:inline-block">Create Recipe </router-link>
            </div>
        </div>
      </span>
    </div>
        <form class="form-inline my-2 my-lg-0">
            <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
    </nav>
  </div>
</template>

<script> 

export default {
    name: "Navbar",
}

</script>

<style>

</style>