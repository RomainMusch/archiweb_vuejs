<template>
  <div id="liste_joueurs">
    <h1 class="sous-titre">Liste des joueurs</h1>
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
            idjoueurs:0,
            nom_joueurs:"",
            age_joueurs:0,
            poste_joueurs:""
        },
        liste_joueurs : [],
        showCreate: false,
    };
  },
  methods: {
    listeJoueurs() {
      axios
        .get("http://localhost:8000/API/joueurs")
        .then((response) => {
          this.liste_joueurs = response.data;
          console.log(this.liste_joueurs);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    ajouterJoueur() {
      axios.post("http://localhost:8000/API/joueurs", this.joueurs).then((response) => {
        console.log(response);
        this.showCreate = false;
        this.listeJoueurs();
      })
      . catch(error => {
        console.log(error)
    });
      console.log("sauvegardé");
    },
    supprimerJoueur(idjoueurs) {
        axios.delete("http://localhost:8000/API/joueurs" + idjoueurs).then((response) => {
            this.listeJoueurs();
            console.log(response.data);
        })
      . catch(error => {
        console.log(error)
    });
      console.log("deleted item " + idjoueurs);
    },
    modifierJoueur(joueurs) {
        console.log(joueurs)
        axios.put("http://localhost:8000/API/joueurs" + joueurs.idjoueurs, joueurs.nom_joueurs, joueurs.age_joueurs, joueurs.poste_joueurs).then((response) => {
           console.log(response.data);
        })
      . catch(error => {
        console.log(error)
    });
      console.log("update item " + joueurs.idjoueurs);
    }
  },
  mounted() {
    console.log("mount");
    axios.get("http://localhost:8000/API/joueurs").then((response) => {
      this.liste_joueurs = response.data;
    });
  },
};
</script>







<style>
#liste_joueurs {
    background-color: #828192;
    margin: 20px auto;
    padding: 10px;
    width: 700px;
}
.sous-titre{
  text-decoration: underline;
}
button {
    color: #fff;
    text-decoration: none;
    background: #b1b8f7;
    padding: 5px;
    border-radius: 5px;
    display: inline-block;
    border: none;
}
</style>