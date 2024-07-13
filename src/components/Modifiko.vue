<template>
  <div class="edit container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Modifiko Vozitesin</h1>
    <form v-on:submit="updatevozites">
        <div class="well">
            <h4>Infot e vozitesit</h4>
            <div class="form-group">
                <label>EmriVozitesit_SMVF</label>
                <input type="text" class="form-control" placeholder="First Name" v-model="vozites.EmriVozitesit_SMVF">
            </div>
            <div class="form-group">
                <label>MbiemriVozitesit_SMVF</label>
                <input type="text" class="form-control" placeholder="Last Name" v-model="vozites.MbiemriVozitesit_SMVF">
            </div>
        </div>
        <div class="well">
            <h4>Detajet e vozitesit</h4>
            <div class="form-group">
                <label>Nr_Vozitesit_SMVF</label>
                <input type="text" class="form-control" placeholder="Nr_Vozitesit_SMVF" v-model="vozites.Nr_Vozitesit_SMVF">
            </div>
            <div class="form-group">
                <label>EkipaVozitesit_SMVF</label>
                <input type="text" class="form-control" placeholder="EkipaVozitesit_SMVF" v-model="vozites.EkipaVozitesit_SMVF">
            </div>
        </div>

        <div class="well">
            <h4>Karriera e vozitesit</h4>
            <div class="form-group">
                <label>PiketVozitesit_SMVF</label>
                <input type="text" class="form-control" placeholder="PiketVozitesit_SMVF" v-model="vozites.PiketVozitesit_SMVF">
            </div>
            <div class="form-group">
                <label>GaratFituara_SMVF</label>
                <input type="text" class="form-control" placeholder="GaratFituara_SMVF" v-model="vozites.GaratFituara_SMVF">
            </div>
            <div class="form-group">
                <label>TruefetFituara_SMVF</label>
                <input type="text" class="form-control" placeholder="TruefetFituara_SMVF" v-model="vozites.TruefetFituara_SMVF">
            </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
    import Alert from './Alert'
    export default {
    name: 'shto',
    data () {
        return {
        vozites: {},
        alert:''
        }
    },
    methods: {
        fetchvozites(id){
            this.$http.get('http://slimapp:8080/api/vozites/'+id)
            .then(function(response){
                this.vozites = response.body;
            });
        },
        updatevozites(e){
            if(!this.vozites.EmriVozitesit_SMVF || !this.vozites.MbiemriVozitesit_SMVF || !this.vozites.Nr_Vozitesit_SMVF){
                this.alert = 'Ju lutem mbushni te gjith rreshtat';
            } else {
                let updvozites = {
                    EmriVozitesit_SMVF: this.vozites.EmriVozitesit_SMVF,
                    MbiemriVozitesit_SMVF: this.vozites.MbiemriVozitesit_SMVF,
                    EkipaVozitesit_SMVF: this.vozites.EkipaVozitesit_SMVF,
                    Nr_Vozitesit_SMVF: this.vozites.Nr_Vozitesit_SMVF,
                    PiketVozitesit_SMVF: this.vozites.PiketVozitesit_SMVF,
                    GaratFituara_SMVF: this.vozites.GaratFituara_SMVF,
                    TruefetFituara_SMVF: this.vozites.TruefetFituara_SMVF
                }

                this.$http.put('http://slimapp:8080/api/vozites/modifiko/'+this.$route.params.id, updvozites)
                    .then(function(response){
                        this.$router.push({path: '/', query: {alert: 'Vozitesi eshte modifikuar'}});
                    });

                e.preventDefault();
            }
            e.preventDefault();
        }
    },
    created: function(){
        this.fetchvozites(this.$route.params.id);
    },
    components:{
        Alert
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
