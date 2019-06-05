<template>
    <div style="padding: 2rem 3rem; text-align: left;">
        <div class="field">
            <label class="label">Name</label>
            <div class="control">
                <input :class="['input', ($v.form.name.$error) ? 'is-danger' : '']" type="text" 
                       v-model="form.name">
            </div>
            <p v-if="$v.form.name.$error" class="help is-danger">This name is invalid</p>
        </div>
        <div class="field">
            <label class="label">Surname</label>
            <div class="control">
                <input :class="['input', ($v.form.surname.$error) ? 'is-danger' : '']" type="text" 
                       v-model="form.surname">
            </div>
            <p v-if="$v.form.name.$error" class="help is-danger">This surname is invalid</p>
        </div>
        <div class="field">
            <label class="label">Email</label>
            <div class="control">
                <input :class="['input', ($v.form.demoEmail.$error) ? 'is-danger' : '']"  type="text" placeholder="Email input" v-model="form.demoEmail">
            </div>
            <p v-if="$v.form.demoEmail.$error" class="help is-danger">This email is invalid</p>
        </div>
          <div class="field">
            <label class="label">Phone</label>
            <div class="control">
                <input :class="['input', ($v.form.phone.$error) ? 'is-danger' : '']" type="text" 
                       v-model="form.phone">
            </div>
            <p v-if="$v.form.phone.$error" class="help is-danger">The Phone is invalid</p>
        </div>
    </div>
</template>

<script>
    import {validationMixin} from 'vuelidate'
    import {required, email} from 'vuelidate/lib/validators'
    export default {
        props: ['clickedNext', 'currentStep'],
        mixins: [validationMixin],
        data() {
            return {
                form: {
                    name: '',
                    demoEmail: '',
                    surname: '',
                    phone:'',
                }
            }
        },
        validations: {
            form: {
                name: {
                    required
                },
                surname: {
                    required
                },
                demoEmail: {
                    required,
                    email
                },
                phone: {
                    required
                }
               
            }
        },
        watch: {
            $v: {
                handler: function (val) {
                    if(!val.$invalid) {
                        this.$emit('can-continue', {value: true});
                    } else {
                        this.$emit('can-continue', {value: false});
                        setTimeout(()=> {
                            this.$emit('change-next', {nextBtnValue: false});
                        }, 3000)
                    }
                },
                deep: true
            },
            clickedNext(val) {
                console.log(val);
                if(val === true) {
                    this.$v.form.$touch();
                }
            }
        },
        mounted() {
            if(!this.$v.$invalid) {
                this.$emit('can-continue', {value: true});
            } else {
                this.$emit('can-continue', {value: false});
            }
        }
    }
</script>