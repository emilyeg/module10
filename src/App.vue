<template>
  <div id="app" class="container">
    <h1>Random Quote Generator</h1>

    <!-- Display the quote or a loading message -->
    <p v-if="loading">Loading...</p>
    <p v-else>"{{ quote }}"</p>

    <!-- The button that triggers the API call -->
    <button @click="getQuote">Get New Quote</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      quote: '',
      loading: false
    };
  },
  methods: {
    async getQuote() {
      this.loading = true; // show the loading message
      try {
        const response = await fetch(
          'https://quotes15.p.rapidapi.com/quotes/random/?language_code=en',
          {
            method: 'GET',
            headers: {
              'x-rapidapi-host': 'quotes15.p.rapidapi.com',
              'x-rapidapi-key': '98e6542a07msh1c2e8d07d2cba11p1fb293jsn10c4bbcae964'
            }
          }
        );
        const data = await response.json();
        this.quote = data.content; // update the quote
      } catch (error) {
        console.error('Error fetching quote:', error);
        this.quote = 'Failed to fetch quote.';
      } finally {
        this.loading = false; // hide the loading message
      }
    }
  },
  mounted() {
    this.getQuote(); // fetch a quote when the page loads
  }
};
</script>



<style>
.container {
  text-align: center;
  font-family: Arial, sans-serif;
  margin-top: 50px;
}
button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
}
.author {
  font-style: italic;
  color: #555;
  margin-top: 5px;
}


</style>
