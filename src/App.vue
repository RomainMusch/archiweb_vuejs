<template>
  <div id="app">
    <h1>FootDiv</h1>
    <ListeJoueurs></ListeJoueurs>
  </div>
</template>

<script>
import ListeJoueurs from './Joueurs'

export default {
  name: 'app',
  components:{ListeJoueurs},
  data () {
      return {};
    },
  methods:{},
  };
</script>

<style>
#app {
	font-family: Helvetica, Arial, sans-serif;
	text-align: center;
	color: #2c3e50;
	background-color: #878f99;
	margin: 10px auto;
	padding: 10px;
}
</style>
