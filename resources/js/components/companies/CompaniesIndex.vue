<template>
    <div>
        <router-link :to="{ name: 'companies.create' }">Create company</router-link>
    </div>
    <ul>
        <li v-for="company in companies" :key="company.id">{{ company.name }} - {{ company.email }} - {{ company.address }} - {{ company.website }} 
            <router-link :to="{ name: 'companies.edit', params: {id: company.id}}">Edit</router-link>
            <button @click="deleteCompany(company.id)" className="bg-red-900">Delete</button>
        </li>
    </ul>
</template>

<script>
import useCompanies from '../../composables/companies';
import { onMounted } from 'vue';

export default {
    setup() {
        const { companies, getCompanies, destroyCompany } = useCompanies()
        onMounted(getCompanies)
        const deleteCompany = async id => {
            if(!window.confirm('Are you sure')) return
            await destroyCompany(id)
            await getCompanies()
        }
        return {
            companies,
            deleteCompany
        }
    }
}

</script>