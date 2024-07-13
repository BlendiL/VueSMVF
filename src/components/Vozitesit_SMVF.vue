<template>
  <div class="vozitesit container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Menaxho vozitesit</h1>
    <input class="form-control" placeholder="Enter MbiemriVozitesit_SMVF" v-model="filterInput">
    <br />
    <table class="table table-striped">
        <thead>
          <tr>
            <th>EmriVozitesit_SMVF</th>
            <th>MbiemriVozitesit_SMVF</th>
            <th>EkipaVozitesit_SMVF</th>
            <th>Nr_Vozitesit_SMVF</th>
            <th>PiketVozitesit_SMVF</th>
            <th>GaratFituara_SMVF</th>
            <th>TruefetFituara_SMVF</th>
            <th></th>
          </tr>
        </thead>
        <tbody style="width: 100%;">
          <tr v-for="vozites in filterBy(vozitesit, filterInput)">
            <td>{{vozites.EmriVozitesit_SMVF}}</td>
            <td>{{vozites.MbiemriVozitesit_SMVF}}</td>
            <td>{{vozites.EkipaVozitesit_SMVF}}</td>
            <td>{{vozites.Nr_Vozitesit_SMVF}}</td>
            <td>{{vozites.PiketVozitesit_SMVF}}</td>
            <td>{{vozites.GaratFituara_SMVF}}</td>
            <td>{{vozites.TruefetFituara_SMVF}}</td>
            <td><router-link class="btn btn-primary" v-bind:to="'/modifiko/'+vozites.ID">Modifiko</router-link> <button class="btn btn-danger" v-on:click="deletevozites(vozites.ID)">Fshi</button></td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert';
  export default {
    name: 'vozitesit',
    data () {
      return {
        vozitesit: [],
        alert:'',
        filterInput:''
      }
    },
    methods: {
      fetchvozitesit(){
        this.$http.get('http://slimapp:8080/api/Vozitesit_SMVF')
          .then(function(response){
            this.vozitesit = response.body;
          });
      },
      filterBy(list, value){
        value = value.charAt(0).toUpperCase() + value.slice(1);
        return list.filter(function(vozites){
          return vozites.MbiemriVozitesit_SMVF.indexOf(value) > -1;
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
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert;
      }
      this.fetchvozitesit();
    },
    updated: function(){
      this.fetchvozitesit();
    },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
