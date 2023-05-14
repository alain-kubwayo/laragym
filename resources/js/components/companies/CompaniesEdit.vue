<template>
    <div v-if="errors !== ''">{{  errors }}</div>
    <form @submit.prevent="saveCompany">
        <input type="text" placeholder="Name" name="name" id="name" v-model="company.name" >
        <input type="text" placeholder="Email" name="email" id="email" v-model="company.email" >
        <input type="text" placeholder="Address" name="address" id="address" v-model="company.address" >
        <input type="text" placeholder="Website" name="website" id="website" v-model="company.website" >
        <button type="submit">Create</button>
    </form>
</template>

<script>
import { onMounted } from 'vue';
import useCompanies from '../../composables/companies';
export default {
    props: {
        id: {
            required: true,
            type: String
        }
    },
    setup(props) {
        const { company, getCompany, updateCompany, errors } = useCompanies()
        onMounted(getCompany(props.id))
        const saveCompany = async () => {
            await updateCompany(props.id)
        }
        return {
            errors,
            company,
            saveCompany
        }
    }
}
</script>