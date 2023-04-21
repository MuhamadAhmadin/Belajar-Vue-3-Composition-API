<template>
    <div class="container my-5">
        <div class="row">
            <div class="d-flex justify-content-between align-items-center">
                <h2>Create Transaction</h2>
                <router-link :to="{ name: 'transaction.index' }" class="btn btn-sm btn-warning">Back</router-link>
            </div>
            <hr>
            <form action="">
                <div class="form-group col-md-12 mb-3">
                    <label>Title</label>
                    <input type="text" class="form-control">
                </div>
                <div class="form-group col-md-12 mb-3">
                    <label>Amount</label>
                    <input type="text" class="form-control">
                </div>
                <div class="form-group col-md-12 mb-3">
                    <label>Type</label>
                    <select name="type" id="type" class="form-control">
                        <option value="expense">Expense</option>
                        <option value="revenue">Revenue</option>
                    </select>
                </div>
                <div class="form-group col-md-12 mb-3">
                    <label>Time</label>
                    <input type="date" class="form-control">
                </div>

                <div class="form-group col-md-12">
                    <button type="submit" class="btn btn-sm btn-primary">Save</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>