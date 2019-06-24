<template>
  <div class="TopContent">
    <ul>
      <li v-for="(user, index) in users" :key="index">
        {{user.born}}
        {{user.first}}
      </li>
    </ul>
  </div>
</template>

<script>
import { firebaseApp, db } from '../firebaseApp'
export default {
  name: 'TopContent',
  data () {
    return {
      users: []
    }
  },
  created() {
    db.collection("users").get().then((querySnapshot) => {
      querySnapshot.forEach((doc) => {
          this.users.push(doc.data())
          console.log(process.env.NODE_ENV)
      });
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
a {
  color: #42b983;
}
</style>
