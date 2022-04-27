<template>

        <div class="sample">
            <form v-if="!formSubmit" @submit.prevent="formSubmit = true">

                 <app-progress
                 :progressWidth="progressWidth">
                 
                 </app-progress>   


                <app-field
                  v-for="(field,i) in info"
                  :key="i"
                  :value="field.value"
                  :name="field.name"
                  :valid="field.valid"
                  @updated="onInput(i, $event)">
                </app-field>

                <button class="btn btn-primary">
                  Send Data
              </button>

                <pre> {{ info }}</pre>

            </form>
            <div v-else>
                <table class="table table-bordered">
                    <tr v-for="(el, i) in info" :key="i">
                        <td>{{ el.name }}</td>
                        <td>{{ el.value}}</td>
                    </tr>
                </table>
            </div>
        </div>

</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css'
import AppField from '@/components/AppField.vue'
import AppProgress from '@/components/AppProgress.vue'

export default {
  name: 'App',
  components: {
    AppField,
    AppProgress
  },
  data: () => ({
    info: [{
        name: 'Name',
        value: '',
        pattern: /^[a-zA-Z ]{2,30}$/
    }, {
        name: 'Phone',
        value: '',
        pattern: /^[0-9]{7,14}$/
    }, {
        name: 'Email',
        value: '',
        pattern: /.+/
    }, {
        name: 'Some Field 1',
        value: '',
        pattern: /.+/
    }, {
        name: 'Some Field 2',
        value: '',
        pattern: /.+/
    }],
    formSubmit: false
}),
computed: {
    progressWidth() {
        let numEl = 0
        // for (let i = 0; i < this.info.length; i++) {
        //     if (this.info[i].value !== '') {
        //         numEl++
        //     }
        // }

        numEl = this.info.reduce((total, field) => {
            return total + (field.valid ? 1 : 0)
        }, 0)

        return numEl * (100 / this.info.length) + '%'
    }
},
methods: {
    onInput(i, value) {
        let field = this.info[i]
        field.value = value
        field.activated = true
        field.valid = field.pattern.test(field.value)


        console.log(field)
        console.log(this.value)
    }
},
created() {
    return this.info.forEach(field => {
        field.valid = field.pattern.test(field.value)
    })
}
}

</script>

<style>

</style>
