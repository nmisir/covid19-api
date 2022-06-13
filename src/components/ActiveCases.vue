<template>
    
</template>

<script>
    export default {
        name: 'ActiveCases',

        components: {},
        data() {
            return {
                arrActive: [],
            }
        },
        methods: {
            async activeCovidCases(country) {
                const url = (`https://api.covid19api.com/live/country/${country}/status/active`)
                const res = await fetch(url)
                const data = await res.json()
                return data
            },

        },

        async created() {
            const data = await this.activeCovidCases()
            this.arrActive = data.Active
        }
    }
</script>