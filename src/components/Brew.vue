<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1 class="text-center text-info">Breweries List</h1>
            </div>
            <!-- /.col-12 -->
        </div>
        <!-- /.row -->
        <div class="row">
            <div class="col-6">
                <BrewList :brews="brews"/>
            </div>
            <!-- /.col-6 -->
            <div class="col-6">
                <BrewMap/>
            </div>
            <!-- /.col-6 -->
        </div>
        <!-- /.row -->
    </div>
    <!-- /.container -->
</template>

<script>
    import axios from "axios";
    import BrewList from "./BrewList.vue";
    import BrewMap from "./BrewMap";

    export default {
        name: "Brew",
        components: {
            BrewList,
            BrewMap
        },

        data: function () {
            return {
                brews: []
            };
        },
        mounted: function () {
            axios.get("https://api.openbrewerydb.org/breweries").then(r => {
                this.brews = r.data;
            });
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
</style>
