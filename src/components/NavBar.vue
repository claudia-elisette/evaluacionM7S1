<template>
    <nav class="navBar">
        <img src="../assets/pokemon.svg" alt="">
    </nav>
</template>

<script>
export default {
    name: 'nav-comp',
    // props: {},
    data: function(){
        return {}
    },
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    nav{
        background-color: rgb(235, 92, 92);
        text-align: center;
    }
    img{
        width: 20rem;
        padding: 1.25rem;
    }
</style>