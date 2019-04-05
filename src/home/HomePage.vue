<template>
    <div>
        <em v-if="users.loading">Loading users...</em>
        <span v-if="users.error" class="text-danger">ERROR: {{users.error}}</span>
        <div class="avatar">
            <i class="fa fa-user-circle"></i>
        </div>
        <div class="hamburger">
            <i class="fa fa-bars"></i>
        </div>
        <div class="buttons">
            <button>Clear Filters</button>
            <button>New Case</button>
        </div>
        <div class="table-list">
            <table>
                <thead>
                    <tr>
                        <th scope="col" style="text-align: left; width: 10rem;">
                            ID
                        </th>
                        <th scope="col" style="text-align: left; width: 20rem;">
                            First Name
                        </th>
                        <th scope="col" style="text-align: left; width: 20rem;">
                            Last Name
                        </th>
                        <th scope="col" style="text-align: left; width: 20rem;">
                            Gender
                        </th>
                        <th scope="col" style="text-align: left; width: 15rem;">
                            Test
                        </th>
                        <th scope="col" style="text-align: left; width: 20rem;">
                            Status
                        </th>
                        <th scope="col" style="text-align: center; width: 10rem;">
                            Actions
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="user in users.items" :key="user.id">
                        <td>{{ user.id }}</td>
                        <td>{{ user.firstName }}</td>
                        <td>{{ user.lastName }}</td>
                        <td>{{ user.gender }}</td>
                        <td>GD</td>
                        <td>Pending</td>
                        <td style="text-align: center;">:</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <p>
            <router-link to="/login">Logout</router-link>
        </p>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            account: state => state.account,
            users: state => state.users.all
        })
    },
    created () {
        this.getAllUsers();
    },
    methods: {
        ...mapActions('users', {
            getAllUsers: 'getAll',
            deleteUser: 'delete'
        })
    }
};
</script>

<style>
.buttons{
    display: flex;
    justify-content: flex-end;
    margin-bottom: 30px;
}
button{
    margin: 0 10px
}
.table-list{
    background-color: #efefef;
    padding: 10px;
    margin-left: 30px
}
.avatar{
    display:flex;
    justify-content: flex-end;
    font-size: 2em
}
.hamburger{
    font-size: 2em
}
</style>