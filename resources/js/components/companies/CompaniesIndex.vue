<template>
    <div class="flex place-content-end mb-4">
    <div class="px-4 py-2 bg-indigo-600 hover:bg-indigo-50 text-indigo-600">
            <router-link :to="{ name: 'companies.create' }" class="text-sm font-medium text-red-400">Create company</router-link>
        </div>
    </div>
    <div class="overflow-hidden overflow-x-auto min-w-full align-middle sm:rounded-md">
        <table class="min-w-full border divide-y divide-gray-200">
            <thead>
            <tr>
                <th class="px-6 py-3 bg-gray-50">
                    <span
                        class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase">Name</span>
                </th>
                <th class="px-6 py-3 bg-gray-50">
                    <span
                        class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase">Email</span>
                </th>
                <th class="px-6 py-3 bg-gray-50">
                    <span
                        class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase">Address</span>
                </th>
                <th class="px-6 py-3 bg-gray-50">
                    <span
                        class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase">Website</span>
                </th>
            </tr>
            </thead>

            <tbody class="bg-white divide-y divide-gray-200 divide-solid">
            <template v-for="item in companies" :key="item.id">
                <tr class="bg-white">
                    <td class="px-6 py-4 text-sm leading-5 text-gray-900 whitespace-no-wrap">
                        {{ item.name }}
                    </td>
                    <td class="px-6 py-4 text-sm leading-5 text-gray-900 whitespace-no-wrap">
                        {{ item.email }}
                    </td>
                    <td class="px-6 py-4 text-sm leading-5 text-gray-900 whitespace-no-wrap">
                        {{ item.address }}
                    </td>
                    <td class="px-6 py-4 text-sm leading-5 text-gray-900 whitespace-no-wrap">
                        {{ item.website }}
                    </td>
                    <td class="px-6 py-4 text-sm text-center leading-5 text-gray-900 whitespace-no-wrap">
                         <router-link :to="{ name: 'companies.edit', params: { id: item.id } }"
                         class="mr-2 text-red-400 p-3 ">Edit</router-link>
                        <button @click="deleteCompany(item.id)"
                                class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150">
                                Delete</button>
                    </td>
                </tr>
            </template>
            </tbody>
        </table>
    </div>
</template>

<script>
import useCompanies from '../../composables/companies'
import { onMounted } from 'vue';

export default {
      setup() {
        const { companies, getCompanies, destroyCompany } = useCompanies()

        const deleteCompany = async (id) => {
            if (!window.confirm('You sure?')) {
                return
            }

            await destroyCompany(id)
            await getCompanies()
        }

        onMounted(getCompanies)

        return {
            companies,
            deleteCompany
        }
    }
}
</script>