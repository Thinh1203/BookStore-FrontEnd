<template>
    <div class="card card-item" style="width: 14rem;">
        <router-link :to="`/product/${item._id}`" style="text-decoration: none; color: inherit;">
        <img :src="`${item.cover}`" height="325" width="225" class="card-img-center cover" alt="...">
        <div class="badges-hot" v-if="item.hot">Hot</div>
        <div class="card-body">
            <p class="card-title">{{ item.title }}</p>
            <p class="card-author">{{ item.author }}</p>
            <p class="card-text">{{ item.price }} vnđ</p>
        </div>
        </router-link>
    </div>
</template>

<script>
export default {
    name:"Item",
    props: [
        "item"
    ]
}
</script>
<style>
.card-item {
    margin: 14px;
    margin-bottom: 20px;
    width: 23%;
}
.card-item:hover {
    background: rgb(236, 95, 95);
}
.card-img-center {
    pointer-events: none;
}
.card-author, .card-title, .card-text  {
    justify-content: center;
    display: flex;
}

.badges-hot {
    position: absolute;
    top: 6px;
    left: 8px;
    background: #f0163a;
    color: #fff;
    padding: 8px;
    border-radius: 50%;
}

</style>