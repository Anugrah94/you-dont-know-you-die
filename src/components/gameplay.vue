<template>
  <div>
    <div class="container" v-if="player.turn === room.turn && room.winner === -1">
      <h2>hi {{player.name}}</h2>
      <h2>point kamu : {{player.point}}</h2>
      <div class="d-flex flex-row">
        <div class="p-3">
          <p style="color:red">Tusuk</p>
          <img src="https://www.shareicon.net/download/2016/10/12/843613_horror_512x512.png" width="30%" @click="useSkill(0)">
          <p>point:10 | damage:10</p>
        </div>
        <div class="p-3">
          <p style="color:red">Tebas</p>
          <img src="https://www.shareicon.net/download/2016/10/01/837948_miscellaneous_512x512.png" width="30%" @click="useSkill(1)">
          <p>point:20 | damage:20</p>
        </div>
        <div class="p-3">
          <p style="color:red">Bacok</p>
          <img src="https://cdn4.iconfinder.com/data/icons/video-game-items-concepts/128/weapon-saber-pirate-512.png" width="30%" @click="useSkill(2)">
          <p>point:30 | damage:30</p>
        </div>
        <div class="p-3">
          <p style="color:red">Cubit</p>
          <img src="http://icons.iconarchive.com/icons/iconsmind/outline/512/Pinch-icon.png" width="30%" @click="useSkill(3)">
          <p>point:40 | damage:40</p>
        </div>
      </div>
      <h1>Terrr-{{room.players[player.turn].action}}</h1>
      <img src="http://webiconspng.com/wp-content/uploads/2017/09/Blood-PNG-Image-69403.png" width="30%" class="flicker-in-1" v-if="room.players[player.turn].action.length>0">
      <h4>Darah tersisa:</h4>
      <div class="progress">                                                           
        <div class="progress-bar progress-bar-striped bg-danger" role="progressbar" :style="{width: player.health+'%'}" aria-valuenow="100" aria-valuemin="0"
          aria-valuemax="100"></div>
      </div>
      <div class="card text-center">
        <div class="card-header">
          <h3>Pertanyaan</h3>
        </div>
        <div class="card-body">
          <h3 class="card-title">Jawab Pertanyaan berikut ini</h3>
          <h2 class="card-text">{{question.pertanyaan}}</h2>
          <button class="btn btn-success" @click="answering('True')">True</button>
          <button class="btn btn-danger" @click="answering('False')">False</button>
          <button class="btn btn-secondary" @click="doneTurn">Lanjut</button>
        </div>
      </div>
    </div>
    <div class="container" v-else-if="player.turn !== room.turn && room.winner === -1">
      <h1>Mohon tunggu sekarang giliran musuh</h1>
      <img src="http://static.zerochan.net/CROWS.ZERO.full.1384713.jpg" alt="">
    </div>
    <div class="container" v-else-if="room.winner === player.turn">
      <h1>selamat kamu telah membantai musuh</h1>
      <img src="http://static.zerochan.net/Takiya.Genji.full.1036507.jpg" alt="">
    </div>
    <div class="container" v-else>
      <h1>Cupuu!! kamu telah dibantai oleh musuh</h1>
      <img src="http://3.bp.blogspot.com/-6M68ZwGmbo4/UFJ1QhQoAkI/AAAAAAAAEDA/HPiZyWdMnnw/s1600/Naruto%2BSD%2BEpisode%2B24.jpg" alt="">
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
    name: 'Gameplay',
    data () {
      return {
          // question:{}
      }
    },
    computed: {
      ...mapState([
          'question',
          'player',
          'room'
      ])      
    },
    methods: {
      answering (answer) {
        this.$store.commit('answering', answer)
      },
      useSkill (skillIndex) {
        this.$store.commit('useSkill', skillIndex)
        if (this.room.winner === this.player.turn) {
          this.$store.commit('updatePlayers')
          this.$store.dispatch('endTurn')
        }
      },
      doneTurn () {
        this.$store.commit('updatePlayers')
        this.$store.dispatch('endTurn')
        this.$store.dispatch('getQuestion')
      },
      decrease: function(){
        return `${this.player.health} + %`
      }
    },
    created () {
      this.$store.dispatch('getGameplayData')
      this.$store.dispatch('getQuestion')
    }
}
</script>

<style scoped>
.flicker-in-1 {
	-webkit-animation: flicker-in-1 2s linear both;
	        animation: flicker-in-1 2s linear both;
}

/* ----------------------------------------------
 * Generated by Animista on 2018-5-17 21:40:39
 * w: http://animista.net, t: @cssanimista
 * ---------------------------------------------- */

/**
 * ----------------------------------------
 * @animation flicker-in-1
 * ----------------------------------------
 */
@-webkit-keyframes flicker-in-1 {
  0% {
    opacity: 0;
  }
  10% {
    opacity: 0;
  }
  10.1% {
    opacity: 1;
  }
  10.2% {
    opacity: 0;
  }
  20% {
    opacity: 0;
  }
  20.1% {
    opacity: 1;
  }
  20.6% {
    opacity: 0;
  }
  30% {
    opacity: 0;
  }
  30.1% {
    opacity: 1;
  }
  30.5% {
    opacity: 1;
  }
  30.6% {
    opacity: 0;
  }
  45% {
    opacity: 0;
  }
  45.1% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  55% {
    opacity: 1;
  }
  55.1% {
    opacity: 0;
  }
  57% {
    opacity: 0;
  }
  57.1% {
    opacity: 1;
  }
  60% {
    opacity: 1;
  }
  60.1% {
    opacity: 0;
  }
  65% {
    opacity: 0;
  }
  65.1% {
    opacity: 1;
  }
  75% {
    opacity: 1;
  }
  75.1% {
    opacity: 0;
  }
  77% {
    opacity: 0;
  }
  77.1% {
    opacity: 1;
  }
  85% {
    opacity: 1;
  }
  85.1% {
    opacity: 0;
  }
  86% {
    opacity: 0;
  }
  86.1% {
    opacity: 1;
  }
  100% {
    opacity: 1;
  }
}
@keyframes flicker-in-1 {
  0% {
    opacity: 0;
  }
  10% {
    opacity: 0;
  }
  10.1% {
    opacity: 1;
  }
  10.2% {
    opacity: 0;
  }
  20% {
    opacity: 0;
  }
  20.1% {
    opacity: 1;
  }
  20.6% {
    opacity: 0;
  }
  30% {
    opacity: 0;
  }
  30.1% {
    opacity: 1;
  }
  30.5% {
    opacity: 1;
  }
  30.6% {
    opacity: 0;
  }
  45% {
    opacity: 0;
  }
  45.1% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  55% {
    opacity: 1;
  }
  55.1% {
    opacity: 0;
  }
  57% {
    opacity: 0;
  }
  57.1% {
    opacity: 1;
  }
  60% {
    opacity: 1;
  }
  60.1% {
    opacity: 0;
  }
  65% {
    opacity: 0;
  }
  65.1% {
    opacity: 1;
  }
  75% {
    opacity: 1;
  }
  75.1% {
    opacity: 0;
  }
  77% {
    opacity: 0;
  }
  77.1% {
    opacity: 1;
  }
  85% {
    opacity: 1;
  }
  85.1% {
    opacity: 0;
  }
  86% {
    opacity: 0;
  }
  86.1% {
    opacity: 1;
  }
  100% {
    opacity: 1;
  }
}

</style>





