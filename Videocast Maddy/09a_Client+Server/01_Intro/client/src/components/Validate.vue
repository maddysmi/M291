<template>
    <div>
      <hr style="width:90%; border-top:3px solid rgb(39,47,49); margin-top: 30px; margin-bottom: 30px">
        <h3>Rechnungs- und Lieferadresse</h3>
        <form @submit.prevent="submitForm" style="width:50%; margin-left:auto; margin-right:auto;">
            <div class="form-group">
                <input type="text" v-model="name" class="form-control" placeholder="Max Mustermann" style="color: #ffffff; margin: 20px 0px 20px 0px; background-color: rgb(32,38,38)">
                <span v-if="!$v.name.required && $v.name.$dirty" class="text-danger">Dies ist ein Pflichtfeld!</span>
                <span v-if="!$v.name.alpha && $v.name.$dirty" class="text-danger">Keine Sonderzeichen!</span>
            </div>

            <div class="form-group">
                <input type="text" v-model="emails" class="form-control" placeholder="max.muster@mustermail.com" style="color: #ffffff; margin: 20px 0px 20px 0px; background-color: rgb(32,38,38)">
                <span v-if="(!$v.emails.required || !$v.emails.email) && $v.emails.$dirty" class="text-danger">Dies ist ein Pflichtfeld!</span>
            </div>

            <div class="form-group">
                <input type="text" v-model="address" class="form-control" placeholder="Musterstrasse 99" style="color: #ffffff; margin: 20px 0px 20px 0px; background-color: rgb(32,38,38)">
                <span v-if="!$v.address.required && $v.address.$dirty" class="text-danger">Dies ist ein Pflichtfeld!</span>
            </div>

            <div class="form-group">
                <input type="text" v-model="ort" class="form-control" placeholder="Musterort" style="color: #ffffff; margin: 20px 0px 20px 0px; background-color: rgb(32,38,38)">
                <span v-if="!$v.ort.required && $v.ort.$dirty" class="text-danger">Dies ist ein Pflichtfeld!</span>
            </div>

            <div class="form-group">
                <input type="text" v-model="plz" class="form-control" placeholder="0000" style="color: #ffffff; margin: 20px 0px 20px 0px; background-color: rgb(32,38,38)">
                <span v-if="(!$v.plz.required || !$v.plz.numeric) && $v.plz.$dirty" class="text-danger">Dies ist ein Pflichtfeld!</span>
            </div>
            <input type="submit" class="btn btn-primary mt-2" >
        </form>
    </div>
</template>


<script>
    import { required, numeric, alpha, email } from 'vuelidate/lib/validators'
    import {mapState} from "vuex"
    export default {
        name: 'Validate',
        computed: mapState(['validate']),

        data: () => ({
            name: '',
            emails: '',
            address:'',
            ort:'',
            plz:'',
        }),
        validations: {
            name: {required, alpha},
            emails: {required, email},
            address: {required},
            ort: {required},
            plz: {required, numeric}
        },
        methods: {
            submitForm() {
                this.$v.$touch();
                if(!this.$v.$invalid) {
                    console.log(`Name: ${this.name}, Email: ${this.emails}, address: ${this.address}, ort: ${this.ort}, plz: ${this.plz} `)
                }
            }
        }
     }
</script>