<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'transaction.create' }"
                    class="btn btn-primary btn-sm rounded shadow mb-3"
                >Add</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Transction List
                    </div>
                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Title</th>
                                    <th>Amount</th>
                                    <th>Type</th>
                                    <th>Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(transaction, index) in transactions" :key="index">
                                    <td>{{ transaction.title }}</td>
                                    <td>{{ transaction.amount }}</td>
                                    <td>{{ transaction.type }}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link 
                                                :to="{ name: 'transaction.edit', params: { id: transaction.id } }"
                                                class="btn btn-primary btn-sm rounded shadow me-1"
                                            >Edit</router-link>
                                            <button @click="destroy(transaction.id, index)" class="btn btn-danger btn-sm rounded shadow">Delete</button>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { onMounted, ref } from 'vue';

export default {
    setup() {
        const transactions = ref([])

        onMounted(async () => {
            let response = await axios.get('http://vuecompovel.test/api/transaction')
                            .then((res) => {
                                transactions.value = res.data.data;
                            })
                            .catch((err) => {
                                console.log("error: " + err);
                            });
        })

        function destroy(id, index) {
            axios.delete(`http://vuecompovel.test/api/transaction/${id}`)
                .then((res) => {
                    transactions.value.splice(index, 1)
                })
                .catch((err) => {
                    console.log("error: " + err);
                });
        }

        return {
            transactions,
            destroy
        }
    }    
}
</script>