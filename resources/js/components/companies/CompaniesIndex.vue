<template>
    <ul>
        <li v-for="company in companies" :key="company.id">{{ company.name }} - {{ company.email }} - {{ company.address }} - {{ company.website }}</li>
    </ul>
</template>

<script>
import useCompanies from '../../composables/companies';
import { onMounted } from 'vue';

export default {
    setup() {
        const { companies, getCompanies } = useCompanies()
        onMounted(getCompanies)
        return {
            companies
        }
    }
}

</script>