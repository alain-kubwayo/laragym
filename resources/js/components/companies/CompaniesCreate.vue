<template>
    <div v-if="errors !== ''">{{  errors }}</div>
    <form @submit.prevent="saveCompany">
        <input type="text" placeholder="Name" name="name" id="name" v-model="form.name" >
        <input type="text" placeholder="Email" name="email" id="email" v-model="form.email" >
        <input type="text" placeholder="Address" name="address" id="address" v-model="form.address" >
        <input type="text" placeholder="Website" name="website" id="website" v-model="form.website" >
        <button type="submit">Create</button>
    </form>
</template>

<script>
import { reactive } from 'vue'
import useCompanies from '../../composables/companies'

export default {
    setup() {
        const form = reactive({
            name: '',
            email: '',
            address: '',
            website: '',
        })

        const { errors, storeCompany } = useCompanies()

        const saveCompany = async () => {
            await storeCompany({...form})
        }
        return {
            form,
            errors,
            saveCompany,
        }
    }
}
</script>