

<template>
    <div>
        <div class="row justify-content-center">
            <div class="col-xl-10 col-lg-12 col-md-9">
                <div class="card shadow-sm my-5">
                    <div class="card-body p-0">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="login-form">
                                    <div class="text-center">
                                        <h1 class="h4 text-gray-900 mb-4">Register</h1>
                                    </div>
                                    <form class="user" @submit.prevent="signup">
                                        <div class="form-group">
                                            <input type="text" class="form-control" id="exampleInputFirstName"
                                                placeholder="Entrez le nom complet" v-model="form.name">
                                            <small class="text-danger" v-if="errors.name">{{ errors.name[0] }}</small>
                                        </div>

                                        <div class="form-group">
                                            <input type="email" class="form-control" id="exampleInputEmail"
                                                aria-describedby="emailHelp" placeholder="Enter Email Address"
                                                v-model="form.email">
                                                <small class="text-danger" v-if="errors.email">{{ errors.email[0] }}</small>
                                        </div>
                                        <div class="form-group">
                                            <input type="password" class="form-control" id="exampleInputPassword"
                                                placeholder="Password" v-model="form.password">
                                                <small class="text-danger" v-if="errors.password">{{ errors.password[0] }}</small>
                                        </div>
                                        <div class="form-group">
                                            <input type="password" class="form-control" id="exampleInputPasswordRepeat"
                                                placeholder="Confirmer mot de passe" v-model="form.password_confirmation">
                                                <small class="text-danger" v-if="errors.password_confirmation">{{ errors.password_confirmation[0] }}</small>
                                        </div>
                                        <div class="form-group">
                                            <button type="submit" class="btn btn-primary btn-block">Register</button>
                                        </div>


                                    </form>
                                    <hr>
                                    <div class="text-center">
                                        <router-link to="login" class="font-weight-bold small">Vous avez déjà un
                                            compte?</router-link>
                                    </div>
                                    <div class="text-center">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script type="text/javascript">

export default {
    created() {
        if (User.loggedIn()) {
            this.$router.push({ name: 'home' })
        }
    },
    data() {
        return {
            form: {
                name: null,
                email: null,
                password: null,
                confirm_password: null,
            },
            errors: {}
        }
    },

    methods: {
        signup() {
            axios.post('/api/auth/signup', this.form)
                .then(res => {
                    User.responseAfterLogin(res)
                    Toast.fire({
                        icon: 'success',
                        title: 'Connexion réussie'
                    })
                    this.$router.push({ name: 'home' })
                })

                .catch(error => this.errors = error.response.data.errors)
            // .catch(
            //     Toast.fire({
            //         icon: 'warning',
            //         title: 'Email ou Mot de passe invalide!'
            //     })
            // )
        }
    }

}

</script>



<style type="text/css"></style>
