<template>
    <div>
        <a @click='goBack'>Go back to user list</a>
        <h1>{{userData.name}}</h1>
        <ul>
            <li>{{userData.email}}</li>
            <li>{{userData.phone}}</li>
            <li>{{userData.website}}</li>
        </ul>
        <router-link :to="postsLink">Posts</router-link>
        <router-link :to="nextUser">Next user</router-link>
    </div>
</template>


<script>
export default {
    name: 'UserProfile',

    data () {
        return {
            userData: {}
        }
    },

    methods: {
        fetchData() {
            fetch(`https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`)
            .then((res) => { return res.json() })
            .then((data) => { this.userData = data })
        },

        goBack() {
            this.$router.push({name: 'home'});
        }
    },

    computed: {
        postsLink() {
            return `/user/${this.$route.params.id}/posts`;
        },

        nextUser() {
            return `/user/${parseInt(this.$route.params.id) + 1}`;
        }
    },

    watch: {
        '$route' : 'fetchData'
    },

    created() {
        this.fetchData();
    }
}
</script>
