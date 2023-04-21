<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-md-8">

                <div class="d-flex justify-content-between align-items-center">
                    <h3>Edit Transaction</h3>
                    <router-link :to="{ name: 'transaction.index' }" class="btn btn-sm btn-warning">Back</router-link>
                </div>
                <hr>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Form Transaction
                    </div>
                    <div class="card-body">
                        <form @submit.prevent="update()">
                            <div class="form-group col-md-12 mb-3">
                                <label>Title</label>
                                <input type="text" v-model="transaction.title" class="form-control">
                                <div v-if="validation.title" class="text-danger">
                                    {{ validation.title[0] }}
                                </div>
                            </div>
                            <div class="form-group col-md-12 mb-3">
                                <label>Amount</label>
                                <input type="number" v-model="transaction.amount" class="form-control">
                                <div v-if="validation.amount" class="text-danger">
                                    {{ validation.amount[0] }}
                                </div>
                            </div>
                            <div class="form-group col-md-12 mb-3">
                                <label>Type</label>
                                <select v-model="transaction.type" id="type" class="form-control">
                                    <option value="expense">Expense</option>
                                    <option value="revenue">Revenue</option>
                                </select>
                                <div v-if="validation.type" class="text-danger">
                                    {{ validation.type[0] }}
                                </div>
                            </div>
                            <div class="form-group col-md-12 mb-3">
                                <label>Time</label>
                                <input type="text" v-model="transaction.time" class="form-control" placeholder="yyyy-mm-dd hh:mm:ss">
                                <div v-if="validation.time" class="text-danger">
                                    {{ validation.time[0] }}
                                </div>
                            </div>
            
                            <div class="form-group col-md-12">
                                <button type="submit" class="btn btn-sm btn-primary">Save</button>
                            </div>
                        </form>
                    </div>
                    </div>
                </div>
        </div>
    </div>
</template>

<script>
import { onMounted, reactive, ref } from 'vue';
import { useRouter, useRoute } from 'vue-router';
import axios from 'axios';
export default {
    setup() {
        // data binding
        let transaction = reactive({
            title: '',
            amount: '',
            type: '',
            time: ''
        });

        const validation = ref([])

        const router = useRouter();
        const route = useRoute();

        onMounted(async () => {
            let response = await axios.get(`http://vuecompovel.test/api/transaction/${route.params.id}`)
                            .then((res) => {
                                transaction.title = res.data.data.title;
                                transaction.amount = res.data.data.amount;
                                transaction.type = res.data.data.type;
                                transaction.time = res.data.data.time;
                            }).catch((err) => {
                                console.log(err);
                            })
        })

        function update() {
            axios.put(`http://vuecompovel.test/api/transaction/${route.params.id}`, transaction)
                .then((res) => {
                    router.push({ name: 'transaction.index' })
                })
                .catch((err) => {
                    validation.value = err.response.data
                })
        }

        return {
            transaction,
            validation,
            router,
            update
        }
    }
}
</script>