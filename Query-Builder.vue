<template>
    <div>
        Find <strong>Github</strong> user:
        <vue-simple-suggest
                v-model="chosen"
                :list="getSuggestions"
                value-attribute="id"
                display-attribute="login"
                :max-suggestions="10"
                :min-length="0"
                :filter-by-query="true">
            <!-- Filter by input text to only show the matching results -->
        </vue-simple-suggest>
    </div>

</template>

<script>
    import VueSimpleSuggest from 'vue-simple-suggest'
    import 'vue-simple-suggest/dist/styles.css' // Optional CSS
    import axios from  'axios';

    export default {
        components: {
            VueSimpleSuggest
        },
        data() {
            return {
                chosen: ''
            }
        },
        methods: {
            getSuggestions(query) {
                return fetch(`https://api.github.com/search/users?q=${query}`)
                    .then(response => response.json())
                    .then(data => {
                        console.log(data.items);
                        return data.items;
                    })
                    .catch(error => console.error(error))
            }
        }
    }
</script>
