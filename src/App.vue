<template>
    <div class="min-h-screen bg-slate-200 font-[Verdana] text-sm">
        <!--title-->
        <MyTitle/>

        <!--search box-->
        <SearchBox @search-term-event="fetchEmails"/>

        <!--items-->
        <EmailItems :emailItems="emails" :term="term"/>
    </div>

    <div v-if="loading">
        <MySpinner/>
    </div>

    <footer class="bg-gray-900 text-white py-4">
        <div class="container mx-auto text-center">
            <p>Copyright © 2023</p>
        </div>
    </footer>

</template>

<script>
  import MyTitle from '@/components/MyTitle';
  import SearchBox from '@/components/SearchBox';
  import EmailItems from '@/components/EmailItems';
  import MySpinner from '@/components/MySpinner';

  // TODO: Move to an environment file
  const BE_URL = "http://localhost:3000";

  export default {
    name: 'App',
    components: {
      MyTitle,
      SearchBox,
      EmailItems,
      MySpinner
    },
    methods: {
      async fetchEmails(term) {
        this.emails = [];

        if (term.trim() === "") {
          return;
        }
        this.loading = true;

        this.term = term;

        try {
          const response = await fetch(BE_URL + "/emailfinder/search/" + term);
          this.emails = await response.json();

        } catch (error) {
          console.error("Unable to make a request to the BE.", error);
          this.loading = false;
        }

        this.loading = false;
      }
    },
    data() {
      return {
        emails: [],
        term: "",
        loading: false
      }
    }
  }
</script>

<style>
    @import "tailwind-styles.css";
</style>
