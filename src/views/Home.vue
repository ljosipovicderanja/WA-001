<template>
  <div class="home">
    <ul>
      <li v-for="item in commits" v-bind:key="item.sha">
        Commit <router-link :to="'/commit/' + item.sha">{{item.sha}}</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src

// JS objekt koji je definicija VUE komponente
export default {
  name: 'Home',
  data() {
    return {
        commits: [],
    }
  },
 async mounted() {
    // izvršava se kada se komponenta pokreće
    
    let rezultat = await fetch("https://api.github.com/repos/vuejs/vue/commits");
     
     let podaci = await rezultat.json()
    
    // of - za array
    // in - za objekt
    for (let item of podaci) {
     console.log(item.sha);
    }
  this.commits = podaci;
  },
};
</script>
