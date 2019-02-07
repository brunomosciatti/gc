<template>
  <div id="app">
    <main class="container player-content">
      <div class="col-xs-12 noPadd player-header">
        <div class="col-xs-3 player-avatar">
          <img
            src="/src/assets/images/avatar.png"
            width="40px"
            title="gc.user.name"
          />
          <h3>{{ gc.user.name }}</h3>
          <h4>GC ID: {{ gc.user.id }}</h4>
        </div>
        <div class="col-xs-6 player-progress">
          <span class="casual">casual <img src="/src/assets/images/pin.svg"/></span>
          <span class="amador">amador <img src="/src/assets/images/pin.svg"/></span>
          <div class="progress">
            <div
              class="progress-bar"
              role="progressbar"
              aria-valuenow="45"
              aria-valuemin="0"
              aria-valuemax="100"
              style="width:45%"
            >
              <span class="sr-only">45% alcançado</span>
            </div>
          </div>
          <span class="comp">competitivo <img src="/src/assets/images/pin.svg"
          /></span>
          <span class="pro">pro <img src="/src/assets/images/pin.svg"/></span>
        </div>
        <div class="player-badges noPadd col-xs-2">
          <ul>
            <li>
              <img
                title="Iniciante"
                src="/src/assets/images/beginner.svg"
                width="40px"
              />
            </li>
            <li>
              <img
                width="29px"
                style="margin-top:3px;"
                v-bind:src="gc.user.patent"
              />
            </li>
            <li>
              <img
                v-bind:title="gc.user.featured_medal.title"
                width="29px"
                style="margin-top:3px; margin-left:5px"
                v-bind:src="gc.user.featured_medal.image"
              />
            </li>
          </ul>
        </div>
        <div class="player-patent col-xs-1 noPadd">
          <img
            title="Ouro 2"
            src="/src/assets/images/patent.png"
            width="55px"
          />
        </div>
      </div>

      <div class="row col-xs-12 row-eq-height">
        <div class="col-xs-6 sv4fun">
          <span>
            <img
              v-bind:title="gc.forfun.title"
              v-bind:src="gc.forfun.image"
              width="28px;"
            />
            <p>4 FUN</p>
          </span>

          <div class="noPadd sv-card" v-for="server in gc.forfun.servers.slice(0, 3)">
            <ul>
              <li>
                <!-- rip clipboard -->
                <a v-bind:href="server.copy" title="Copiar IP"><i class="far fa-copy"></i></a>
              </li>
              <li>
                <a v-bind:href="server.join" title="Entrar no servidor"><i class="fas fa-sign-in-alt"></i></a>
              </li>
            </ul>
            <span class="sv-name">#{{server.id}} - {{server.title}} </span>
            <span class="sv-mode">{{server.mode}}</span>
            <span class="sv-map">{{server.map}} <em>{{server.current}}/{{server.max}}</em></span>
            <div class="progress">
              <div class="progress-bar" role="progressbar" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100" style="width:50%">
                <span class="sr-only">50% ocupado</span>
              </div>
            </div>
          </div>



        </div>
        <div class="col-xs-3 lobby">
          <span
            ><img
              title="LOBBY"
              src="/src/assets/images/lobby.svg"
              width="20px"
            /> <!-- ok it could dynamic like pice of cake... <3 but... -->
            <p>{{gc.games[0].title}}</p></span>
          <div class="card-stats col-md-4">
            <h3 class="partidas">{{gc.games[0].matches}}</h3>
            <h4>partidas</h4>
          </div>
          <div class="card-stats col-md-4">
            <h3 class="vitorias">{{gc.games[0].win}}</h3>
            <h4>vitórias</h4>
          </div>
          <div class="card-stats col-md-4">
            <h3 class="derrotas">{{gc.games[0].lose}}</h3>
            <h4>derrotas</h4>
          </div>
          <a v-bind:href="gc.games[0].cta.link" title="Ir para o lobby">{{gc.games[0].cta.title}}</a>
        </div>

        <div class="col-xs-3 ranked">
          <span
            ><img
              title="RANKED OPEN"
              src="/src/assets/images/Open.svg"
              width="20px"
            />
            <p>{{gc.games[1].title}}</p></span
          >
          <div class="card-stats col-md-4">
            <h3 class="partidasRanked">{{gc.games[1].matches}}</h3>
            <h4>partidas</h4>
          </div>
          <div class="card-stats col-md-4">
            <h3 class="vitorias">{{gc.games[1].win}}</h3>
            <h4>vitórias</h4>
          </div>
          <div class="card-stats col-md-4">
            <h3 class="derrotas">{{gc.games[1].lose}}</h3>
            <h4>derrotas</h4>
          </div>
          <a v-bind:href="gc.games[1].cta.link" title="Entrar na fila"><em><i class="fas fa-users"></i> 15</em> {{gc.games[1].cta.title}}</a>
        </div>
        <div class="col-xs-12 noPadd footer">
          <a href="#"
            ><i class="fas fa-download"></i>Download Gamers Club Anti-Cheat</a>
          <div class="gc-info">
            <span>{{ gc.online }}</span>
            <p>Jogadores<em>Online</em></p>
            <div class="ban">
              <span>{{ gc.latest_banned }}</span>
              <p>Cheaters Banidos<em>Nos Últimos 7 dias</em></p>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    gc: {
    }
    return {
      online: "",
      name: {},
      gc: {},

      user: {
        name: "",
        id: "",
        expertise: "",
        is_subscriber: "",
        patent: "",
        level: "",
        game_position: {
          id: "",
          title: "",
          image: ""
        },
        featured_medal: {
          id: "",
          title: "",
          image: ""
        }
      },

      games: {
        title: "",
        cta: {
          title: "",
          link: ""
        }
      }
    };
  },
  mounted() {
    axios
      .get("https://api.myjson.com/bins/qs4ao")
      .then(response => {
        this.gc = response.data;
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
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
  background-color: #35495e;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: 0.02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}

button {
  background: #51b767;
  color: #ffffff;
  padding: 15px;
  border-radius: 0;
  font-weight: bold;
  font-size: 15px;
  border: 0;
}

.cards {
  background: #f5f5f5;
  height: 400px;
}
.cards:hover {
  transform: translateY(-0.5em);
  background: #ebebeb;
}

.cards {
  column-count: 1;
  column-gap: 1em;
  margin-top: 70px;
}
</style>
