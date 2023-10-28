<template>
    <button>offset: {{ offset }} query: {{ query }} limit: {{ limit }}</button>
</template>

<script>
export default {
    name : "PaginationButton",

    props: ["offset", "limit", "query"]
}
</script>

<style>

</style>