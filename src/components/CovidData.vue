<template>
    <div>
        <div class="box">
            <h3>Cases</h3>

            <div>
                <span>New:</span>
                {{ numWithCommas(stats.NewConfirmed) }}
            </div>
            <div>
                <span>Total:</span>
                {{ numWithCommas(stats.TotalConfirmed) }}
            </div>
        </div>

        <div class="box">
            <h3>Recovered</h3>

            <div>
                <span>New:</span>
                {{ numWithCommas(stats.NewRecovered) }}
            </div>
            <div>
                <span>Total:</span>
                {{ numWithCommas(stats.TotalRecovered) }}
            </div>
        </div>

        <div class="box">
            <h3>Deaths</h3>

            <div>
                <span>New:</span>
                {{ numWithCommas(stats.NewDeaths) }}
            </div>
            <div>
                <span>Total:</span>
                {{ numWithCommas(stats.TotalDeaths) }}
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'CovidData',
        props: ['stats'],
        methods: {
            numWithCommas(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');
            }
        }
    }
</script>

<style>
.box{
    border: 2px solid;
    padding: 2px;
    margin: 5px;
    width: 250px;
    text-align: center;
}

</style>