<script>
export default {
  data() {
    return {
      league: []
    }
  },
  methods: {
    async getData() {
      const res = await fetch('http://localhost:3000/api/league/get/643eeb212c5958f952816d4c')

      console.log(res)
      
      const data = await res.data
      
      console.log(data)

      return data
    }
  },
  async created() {
    this.league = await this.getData()
  },
};
</script>

<template>
  <div class="border rounded p-3 top-25 start-50">
    <h1>
      <!-- Hard to Handle P+ seeding league -->
      {{ league.name }}
    </h1>
    <p>
      Een netplay league waar iedereen een keer tegen iedereen speelt om de seeding voor het toernooi bij Tjon te bepalen
    </p>
    <h5>Deelnemers:</h5>
    <ul>
      <li>Vincent</li>
    </ul>
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
