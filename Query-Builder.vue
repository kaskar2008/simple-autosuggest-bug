<template>
    <div>
        Find <strong>Github</strong> user:
        <vue-simple-suggest
                v-model="chosen"
                :list="suggestArray"
                value-attribute="id"
                display-attribute="login"
                :max-suggestions="10"
                :debounce="1"
                :min-length="0"
                :filter-by-query="true">
            <input v-model="text">
            <!-- Filter by input text to only show the matching results -->
        </vue-simple-suggest>

        <br>

        <ul v-for="suggest in suggestArray">
            <li>
                {{suggest.login}}
            </li>
        </ul>
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
                chosen: '',
                text:'',
                suggestArray:[]
            }
        },
        watch:{
            text(query) {
                fetch(`https://api.github.com/search/users?q=${query}`)
                    .then(response => response.json())
                    .then(data => {
                        console.log(data.items);
                        this.suggestArray = data.items;

                    })
                    .catch(error => console.error(error))

            }

        },
        methods: {

        }
    }
</script>
