<template>
  <div id="liste_joueurs">
    <h1>Liste des joueurs</h1>
    <p>
      <button v-on:click="showCreate = !showCreate" >
        Ajouter un joueur
      </button>
    </p>
    <div v-if="showCreate">
        <form>
            <label> Nom du joueur: </label> </br>
            <input type="text" id="nom_joueurs" name="nom_joueurs" v-model="joueurs.nom_joueurs" required></br></br>

            <label> Age du joueur: </label> </br>
            <input type="int" id="age_joueurs" name="age_joueurs"v-model="joueurs.age_joueurs" required></br></br>

            <label> Poste du joueur: </label> </br>
            <input type="text"  id="poste_joueurs" name="poste_joueurs"v-model="joueurs.poste_joueurs" required><br></br>

            <button v-on:click="ajouterJoueur()">Sauvegarder</button>

        </form>
    </div>

    <div v-for="joueurs in liste_joueurs" v-bind:key="joueurs.idjoueurs">
        <Joueur v-bind:joueurs="joueurs" @event_delete="supprimerJoueur"  @event_update="modifierJoueur"></Joueur>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Joueur from "./Joueur.vue";
import NouveauJoueur from "./NouveauJoueur.vue";

export default {
  components: { Joueur, NouveauJoueur },
  data() {
    return {
        joueurs:
        {
            age_joueurs:0,
            idjoueurs:0,
            nom_joueurs:"",
            poste_joueurs:""
        },
        liste_joueurs: [],
        uri: "http://localhost:8000/API/joueurs",
        showCreate: false,
    };
  },
  methods: {
    get_liste_joueurs() {
      axios
        .get(this.uri)
        .then((res) => {
          this.liste_joueurs = res.data;
          console.log(this.liste_joueurs);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    ajouterJoueur() {
      axios.post(this.uri, this.joueurs).then((res) => {
        console.log(res);
        this.showCreate = false;
        this.get_liste_joueurs();
      })
      . catch(error => {
        console.log(error)
    });
      console.log("sauvegardé");
    },
    supprimerJoueur(idjoueurs) {
        axios.delete(this.uri + idjoueurs).then((res) => {
            this.get_liste_joueurs();
            console.log(res.data);
        })
      . catch(error => {
        console.log(error)
    });
      console.log("deleted item " + idjoueurs);
    },
    modifierJoueur(joueurs) {
        console.log(joueurs)
        axios.put(this.uri + joueurs.idjoueurs, joueurs.nom_joueurs, joueurs.age_joueurs, joueurs.poste_joueurs).then((res) => {
           console.log(res.data);
        })
      . catch(error => {
        console.log(error)
    });
      console.log("update item " + joueurs.idjoueurs);
    }
  },
  mounted() {
    console.log("mount");
    axios.get(this.uri).then((res) => {
      this.liste_joueurs = res.data;
    });
  },
};
</script>







<style>
#liste_joueurs {
    background-color: #a2b9bc;
    margin: 10px auto;
    padding: 10px;
    width: 500px;
}
button {
    color: #fff;
    text-decoration: none;
    background: #6b5b95;
    padding: 5px;
    border-radius: 5px;
    display: inline-block;
    border: none;
}
</style>