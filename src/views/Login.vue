<template>

    <v-container
            fill-height
            fluid
            grid-list-xl>
        <v-layout
                justify-center
                wrap
        >
            <v-flex
                    xs12
                    md8

            >
<div id="notification">
    <template v-for="(child, index) in children">
        <material-notification
                class="mb-3"
                color="error"
                dismissible
        >

            {{child}}
        </material-notification>
    </template>
</div>

                <material-card
                        color="green"
                        title="Login"
                        text="Enter you credentials"
                >
                    <v-form>
                        <v-container py-0>
                            <v-layout wrap>

                                <v-flex
                                        xs12
                                        md12
                                >
                                    <v-text-field
                                            v-model="email"
                                            class="purple-input"
                                            label="Email"
                                    />
                                </v-flex>
                                <v-flex
                                        xs12
                                        md12
                                >
                                            <v-text-field
                                            v-model="password"
                                            label="Password"
                                            tyPE="password"
                                            class="purple-input"/>
                                </v-flex>

                                <v-flex
                                        xs12
                                        text-xs-right
                                >
                                    <v-btn
                                            class="mx-0 font-weight-light"
                                            color="success"
                                            v-on:click="login"
                                    >
                                        Login
                                    </v-btn>
                                </v-flex>
                            </v-layout>
                        </v-container>
                    </v-form>
                </material-card>
            </v-flex>

        </v-layout>
    </v-container>

</template>

<script>
    import axios from "axios"
    export default {
        name: "Login",
        created(){
            if((this.$router.currentRoute.name=="Login")&&this.owner){
                window.location.href="/"
            }
            return console.log(this.$router.currentRoute.name)
        },
        data(){
        return {
          email:"",
          password:"",
            owner:localStorage.getItem("owner"),
            showErrMessage:false,
            errMessage:"",
            children: []
        }},
    methods:{
            async login(){
            let result=   await axios.post("http://mean-app-tutorial.herokuapp.com/users/auth",{
                    "email": this.email,
                    "password": this.password
                },{})
                if(result.data.success){
                    console.log(result  )
                    localStorage.setItem("owner",result.data.user.id)
                    localStorage.setItem("token","Bearer "+result.data.token)
                }else {

                    this.errMessage=result.data.message
                    this.showErrMessage=true
                    this.children.push(result.data.message);



                }


            }
    }
    }
</script>

<style scoped>

</style>
