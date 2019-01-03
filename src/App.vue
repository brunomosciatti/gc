<template>
  <div id="app">
    <div class="title-section">
      <div class="container">
        <h2>Novo Herói</h2>
      </div>
    </div>
    <main class="container">
      <div class="row">
	  <form role="form" id="frmNovoHeroi">
        <div class="form-group col-xs-10 col-sm-4 col-md-4 col-lg-6">
            <label for="frmNome">Nome</label>
            <input v-model="hero.name" type="text" class="form-control" id="frmNome">
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-4 col-lg-3">
            <label for="frmEspecialidades">Especialidades</label>
            <select v-model="hero.speciality" name="frmEspecialidades" id="frmEspecialidades" class="form-control" tabindex="12">
                <option>Selecione uma especialidade</option>
                <option v-for="x in specialities" :value="x.id">{{ x.name }}</option>

            </select>
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-4 col-lg-3">
            <label for="frmClasse">Classe</label>
            <select v-model="hero.class_id" name="frmClasse" id="frmClasse" class="form-control" tabindex="12">
              <option>Selecione uma classe</option>
                <option v-for="y in classes" :value="y.id">{{ y.name }}</option>

            </select>
        </div>
        <div class="clearfix"></div>
        <div class="form-group col-xs-10 col-sm-4 col-md-2 col-lg-2">
            <label for="frmVida">Vida</label>
            <input type="number" class="form-control" v-model="hero.health_points" id="frmVida">
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-2 col-lg-2">
            <label for="frmDefesa">Defesa</label>
            <input v-model="hero.defense" type="number" class="form-control" id="frmDefesa" >
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-2 col-lg-2">
            <label for="frmDano">Dano</label>
            <input v-model="hero.damage" type="number" class="form-control" id="frmDano" >
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-2 col-lg-3">
            <label for="frmVelAtk">Velocidade de ataque</label>
            <input v-model="hero.attack_speed" type="number" class="form-control" id="frmVelAtk" >
        </div>
        <div class="form-group col-xs-10 col-sm-4 col-md-2 col-lg-3">
            <label for="frmVelMov">Velocidade de movimento</label>
            <input v-model="hero.movement_speed" type="number" class="form-control" id="frmVelMov" >
        </div>
        <div class="clearfix"></div>

        <div class="col-xs-10 col-sm-4 col-md-4 col-lg-4">
            <button @click="postNow()" type="button" class="btn btn-default">Submit</button>
        </div>
    </form>
    <div class="clearfix"></div>


	</div>

  <div class="row">
    <!-- dropzone -->
    <h1>{{hero.class_id}}</h1>
    <h1>{{hero.movement_speed}}</h1>
    <h1>{{hero.atack_speed}}</h1>
    <h1>{{hero.damage}}</h1>
    <h1>{{hero.defense}}</h1>
    <h1>{{hero.name}}</h1>



  </div>




        </main>
      </div>
</template>

<script>
import axios from 'axios';

export default {


 name: 'app',
 data () {
   return {
     hero: {
       name: '',
       speciality: '',
       class_id: '',
       health_points: '',
       defense:'',
       attack_speed: '',
       movement_speed: ''
     },
     specialities: [],
     loading: false,
     classes: [],
   }
 },
 methods: {
   postNow() {
      axios.post('http://heroes.qanw.com.br/heroes', {
         headers: {
            'Content-type': 'application/json',
          },
            class_id: this.hero.class_id,
            name: this.hero.name,
            health_points: this.hero.health_points,
            defense: this.hero.defense,
            attack_speed: this.hero.attack_speed,
            movement_speed: this.hero.movement_speed,
            specialities: this.hero.speciality
           }
         ).then(function(data){
           console.log(data);
         });
        },
      },
 mounted () {
    axios
      .get('http://heroes.qanw.com.br:7625/specialties')
      .then(response => {
        this.specialities = response.data
      })
      axios
      .get('http://heroes.qanw.com.br:7625/classes')
      .then(response => {
        this.classes = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}

</script>

<style>
body {
 margin: 0;
}

#app {
 font-family: 'Avenir', Helvetica, Arial, sans-serif;
 -webkit-font-smoothing: antialiased;
 -moz-osx-font-smoothing: grayscale;
 color: #2c3e50;
}

main {
 text-align: center;
 margin-top: 40px;
}

header {
 margin: 0;
 height: 56px;
 padding: 0 16px 0 24px;
 background-color: #35495E;
 color: #ffffff;
}

header span {
 display: block;
 position: relative;
 font-size: 20px;
 line-height: 1;
 letter-spacing: .02em;
 font-weight: 400;
 box-sizing: border-box;
 padding-top: 16px;
}


button {
 background: #51B767;
 color: #ffffff;
 padding: 15px;
 border-radius: 0;
 font-weight: bold;
 font-size: 15px;
 border: 0;
}

.cards {
 background: #F5F5F5;
 height:400px;
}
.cards:hover {
 transform: translateY(-0.5em);
 background: #EBEBEB;
}


.cards {
  column-count: 1;
 column-gap: 1em;
   margin-top: 70px;

}
</style>
