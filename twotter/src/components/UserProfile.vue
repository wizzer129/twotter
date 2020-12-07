<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">{{ fullName }}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

            <h3 class="user-profile__username">@{{ user.username }}</h3>
            <div class="user-profile__follower-count"><strong>Followers:</strong> {{ followers }}</div>
        </div>
        <div class="user-profile__twoots-wrapper">
            <TwootItem
                v-for="twoot in user.twoots"
                :key="twoot.id"
                :username="user.username"
                :twoot="twoot"
                @favorite="toggleFavorite"
            />
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem';

export default {
    name: 'UserProfile',
    components: { TwootItem },
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                username: '_AlexLazo',
                firstName: 'Alex',
                lastName: 'Lazo',
                email: 'alazo@alazo.io',
                isAdmin: true,
                twoots: [
                    { id: 1, content: 'Twotter is amazing' },
                    { id: 2, content: "Don't forget to subscribe to the earth is square" },
                ],
            },
        };
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowerCount) {
                console.log(`${this.user.username} has gained a follower`);
            }
        },
    },
    computed: {
        fullName() {
            return `${this.user.firstName} ${this.user.lastName}`;
        },
    },
    methods: {
        followUser() {
            this.followers++;
        },
        toggleFavorite(id) {
            console.log('Favorited Tweet', id);
        },
    },

    mounted() {
        this.followUser();
    },
};
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe4e8;
}

.user-profile__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
}

h1 {
    margin: 0;
}
</style>
