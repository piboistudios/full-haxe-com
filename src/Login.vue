<template lang="pug">
    v-card.elevation-5.pa-5(light)
        //v-img.ma-auto.white(
                :src="view.haxe_logo"
                aspect_ratio="4/3"
                width="40%"
            )
        v-card-title 
            div
                h3.baseline.mb-0 Login
        v-card.ma-5(tile)
            v-text-field.mx-5(label="Username" v-model="input.username")
            v-text-field.mx-5(label="Password" type="password" v-model="input.password")
        v-card-actions
            v-btn(color="primary" @click="login") Sign-In
            
</template>

<script>
const md5 = require('md5');
const axios = require('axios');
export default {
    data() {
        return {
            view: {
                haxe_logo: 'data:image/png;base64,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'
            },
            input: {
                username: '',
                password: '',
            }
        }
    },
    methods: {
        login() {
            axios.post('/auth/login', {
                username: this.input.username,
                passHash: md5(this.input.password)
            })
                .then(response => {
                    console.log(response.data);
                })
        }
    }
}
</script>
