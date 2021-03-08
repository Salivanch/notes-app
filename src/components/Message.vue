<template>
    <p>{{message}}</p>
</template>

<script>
export default {
    props:{
        message: {
            type: String,
        },
    },
}
</script>

<style lang="sass" scoped>
p
    color: red
    text-align: center
</style>