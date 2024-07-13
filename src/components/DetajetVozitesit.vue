<template>
  <div class="details container">
    <router-link to="/">Kthehu</router-link>
    <h1 class="page-header">{{vozites.EmriVozitesit_SMVF}} {{vozites.MbiemriVozitesit_SMVF}}
        <span class="pull-right">
            <router-link class="btn btn-primary" v-bind:to="'/modifiko/'+vozites.ID">Modifiko</router-link>
            <button class="btn btn-danger" v-on:click="deletevozites(vozites.ID)">Fshi</button>
            </span>
    </h1>
    <ul class="list-group">
            <li class="list-group-item"><span class="glyphicon glyphicon-EkipaVozitesit_SMVF" aria-hidden="true"></span> {{vozites.EkipaVozitesit_SMVF}}</li>
            <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{vozites.Nr_Vozitesit_SMVF}}</li>
        </ul>

        <ul class="list-group">
            <li class="list-group-item"> {{vozites.PiketVozitesit_SMVF}}</li>
            <li class="list-group-item">{{vozites.GaratFituara_SMVF}}</li>
            <li class="list-group-item">{{vozites.TruefetFituara_SMVF}}</li>
        </ul>
  </div>
</template>

<script>
export default {
  name: 'vozitesdetails',
  data () {
    return {
      vozites: ''
    }
  },
  methods:{
      fetchvozites(id){
          this.$http.get('http://slimapp:8080/api/vozites/'+id)
          .then(function(response){
            this.vozites = response.body;
          });
      },
      deletevozites(id){
          this.$http.delete('http://slimapp:8080/api/vozites/fshi/'+id)
          .then(function(response){
            this.$router.push({path: '/', query: {alert: 'Vozitesi eshte fshier'}});
          });
      }
  },
  created: function(){
      this.fetchvozites(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
