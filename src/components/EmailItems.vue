<template>
    <div class="grid grid-cols-1">
        <div class="grid gap-y-3 my-8 w-full sm:w-3/4 justify-self-center">
            <div :key="email.id" v-for="email in emailItems">
                <EmailItem :emailItem="email" :term="term"/>
            </div>
        </div>
    </div>
</template>

<script>
  import EmailItem from '@/components/EmailItem';

  export default {
    name: "EmailItems",
    components: {EmailItem},
    props: {
      emailItems: Array,
      term: String
    }
  }
</script>

<style scoped>

</style>