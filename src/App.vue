<template>
  <div id="app">
    <h1> ◄ FootDiv ► </h1>
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
	color: #f9f7f8;
	background-color: #383a3b;
	margin: 10px auto;
	padding: 10px;
}
</style>
