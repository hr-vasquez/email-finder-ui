<template>
    <div class="grid grid-cols-1">
        <input class="col-span-1 my-3.5 w-10/12 sm:w-3/4 justify-self-center h-12 border-2
        border-primary rounded-md focus:outline-none text-black text-lg pr-5 px-4" type="search"
        name="search" placeholder="Search" v-model="searchValue" @keyup.enter="findTerm" @input="validateInput"/>
    </div>
</template>

<script>
  export default {
    name: "SearchBox",
    methods: {
      findTerm() {
        this.$emit("search-term-event", this.searchValue);

      },
      /*It should only receive characters*/
      validateInput(event) {
        const regex = /^[a-zA-Z\s]+$/;
        if (!regex.test(event.target.value) && event.target.value !== "") {
          event.target.value = this.inputValue;
        } else {
          this.inputValue = event.target.value;
        }
      }
    },
    data() {
      return {
        searchValue: ""
      }
    }
  }
</script>

<style scoped>

</style>