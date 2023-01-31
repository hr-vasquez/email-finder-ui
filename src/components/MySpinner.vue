<template>
    <div class="fixed top-0 left-0 bottom-0 right-0 flex items-center justify-center bg-gray-200">
        <div class="spinner box-border h-16 w-16 rounded-full border-2 border-t-[#07d] border-b-[#07d]"></div>
    </div>
</template>

<script>
  export default {
    name: "MySpinner"
  }
</script>

<style scoped>
    .spinner {
        animation: spinner .8s ease infinite;
    }

    @keyframes spinner {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(360deg);
        }
    }
</style>