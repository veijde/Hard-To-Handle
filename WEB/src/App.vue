<script>
export default {
  data() {
    return {
      league: {},
      name: '',
      loading: true
    }
  },
  methods: {
    async getData() {
      const res = await fetch('https://h2h-api.onrender.com/api/league/get/643eeb212c5958f952816d4c')
      const data = await res.json()
      this.loading = false;
      return data
    },

    async AddParticipant(e) {
      e.preventDefault()
      if (!this.name) {
        alert('Makker...')
        return
      }

      this.league.participants = [...this.league.participants, this.name]

      const res = await fetch('https://h2h-api.onrender.com/api/league/update/643eeb212c5958f952816d4c', {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(this.league)
      })
    }
  },
  async created() {
    this.league = await this.getData()
  },
};
</script>

<template>
  <div class="d-flex justify-content-center">
    <div class="border rounded p-3">
      <div v-if="loading" class="justify-content-center">
        <h1>ff wachten makker</h1>
        <p>Ik ben gierig dus de data staat op een gratis host die elke 15 minuten zonder activiteit in standby gaat lmao. Je hoeft niet te refreshen ofzo. Shit is dynamisch</p>
      </div>
      <div v-else>
        <h1>
          {{ league.name }}
        </h1>
        <p>
          {{ league.description }}
        </p>
        <p>Vanaf dat iedereen die mee wilt doen in de lijst staat kijken we wel ff wanneer. Dan gooi ik ook al deze inschrijf rommel weg en zet ik hier de regels en het formaat.</p>
        <h5>Wat heb je nodig om mee te doen?</h5>
        <ul class="m-1">
          <li><a href="https://projectplusgame.com/download">P+ 2.3.2</a></li>
          <li><a href="https://vimm.net/vault/18177">Brawl ISO</a></li>
          <li><a href="https://www.smashladder.com/guides/view/26oz/controller-guide-2-0">Gamecube controller en een GCC adapter</a></li>
          <li>Internet enzo</li>
        </ul>
        <br>
        <h5>Deelnemers:</h5>
        <ul class="m-1" v-for="participant in league.participants">
          <li>{{ participant }}</li>
        </ul>
        <div>
          <form @submit="AddParticipant">
            <input v-model="name" name="name" type="text" class="m-3">
            <button class="m-3 p-2 border-0 rounded" style="background-color: rgb(0, 189, 126); color: rgb(24, 24, 24);">Ayyy ik doe ook mee 😎</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
