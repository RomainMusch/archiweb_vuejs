<template>
    <div class="joueur">

            <h3><span v-if="showInput==false">
                <h4> {{joueurs.nom_joueurs}} ({{joueurs.age_joueurs}} ans, {{joueurs.poste_joueurs}})</h4>
                <button v-on:click="showInput=true">Modifier</button> 
                </span>
            </h3>

            <span v-if="showInput">
                <form>
                    <label> Nom du joueur: </label> </br>
                    <input type="text" id="nom_joueurs" name="nom_joueurs" v-model="joueurs.nom_joueurs"></br>

                    <label> Age du joueur: </label> </br>
                    <input type="int" id="age_joueurs" name="age_joueurs"v-model="joueurs.age_joueurs"></br>

                    <label> Poste du joueur: </label> </br>
                    <input type="text"  id="poste_joueurs" name="poste_joueurs"v-model="joueurs.poste_joueurs"><br>

                    <button v-on:click="modifierJoueur(joueurs)"> Sauvegarder </button> 
                </form>
            </span>

            <button v-on:click="supprimerJoueur(joueurs.idjoueurs)"> Supprimer </button>

    </div> 
</template>
<script>
    export default {
        name: 'Joueur',
        props: ['joueurs'],
        data() {
            return {
                showInput: false
            }
        },
        methods: {
            supprimerJoueur(idjoueurs) {
                console.log(idjoueurs)
                this.$emit('event_delete', idjoueurs);
            },
            modifierJoueur(joueurs) {
                this.$emit('event_update', joueurs);
                this.showInput = false;
            }
        }
    }
</script>
<style >
    .joueur {
        background-color:lightgrey;
        width: 400px;
        margin: 5px auto;
        padding : 5px;
    }
    button:hover{
        background-color: blue;
        color:white;
        cursor:pointer;
    }
</style>