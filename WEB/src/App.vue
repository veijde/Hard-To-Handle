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
      this.name = '';
    }
  },
  async created() {
  },
};
</script>

<template>
  <div class="d-flex justify-content-center">
    <div class="border rounded p-3">
      <h1>
        Hard to Händel P+ seeding league
      </h1>
      <br>
      <h5>Regels</h5>
      <ul class="m-1">
        <li>Alle potjes zijn best of 3</li>
        <li>Standaard stagelist. Random stages om het fast en fun te houden</li>
      </ul>
      <br>
      <h5>Wanneer</h5>
      <p>Best ff kijken of we 1 dag kunnen vinden waarop de meeste mensen kunnen om zo veel mogelijk potjes dan te doen.</p>
      <p>Als we niet alles kunnen doen kunnen we kijken voor een tweede dag of kunnen we de rest van de potjes gewoon laten
        doorgaan wanneer de twee mensen de nog moeten spelen kunnen.</p>
      <br>
      <h5>Nodig om mee te doen</h5>
      <ul class="m-1">
        <li><a href="https://projectplusgame.com/download">P+ 2.3.2</a></li>
        <li><a href="https://vimm.net/vault/18177">Brawl ISO</a></li>
        <li><a href="https://www.smashladder.com/guides/view/26oz/controller-guide-2-0">Gamecube controller en een GCC
            adapter</a></li>
        <li>Internet enzo</li>
      </ul>
      <br>
      <div class="justify-content-center">
        <iframe class="d-block justify-content-center" src="https://challonge.com/nl/5f5wbzhc/module?theme=2&match_width_multiplier=0.5&show_standings=1"
          width="100%" height="500" frameborder="0" scrolling="auto"></iframe>
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
}</style>
