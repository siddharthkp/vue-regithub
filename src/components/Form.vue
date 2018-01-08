<template>
  <div>
    <div class="form">
      <input v-model="username" src="text" placeholder="enter username"/>
      <button @click="onClick" :disabled="username.length < 1">See profile</button>
    </div>
    <div v-if="repos.length > 0" class="section repositories">
      <div class="repo" v-for="repo in repos">
        <a
          class="name"
          :href="repo.url"
        >
            {{repo.name}}
          </a>
        <div class="stars">
          {{repo.stars}}
        </div>
        <div class="clear"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'form',
  data() {
    return {
      username: '',
      repos: []
    }
  },
  methods: {
    onClick: function() {
      let component = this
      this.axios
        .get('https://github-user.now.sh/?username=' + this.username)
        .then(function(response) {
          component.repos = response.data.repos
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
