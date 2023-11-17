<template>
    <div
          class="grid-container"
          v-if="getProducts.data && getProducts.data['hydra:member']"
        >
    <div class="button">
        <button @click="open_admin()" class="category">Product</button>
        <button @click="open_categories()" class="category">Categories</button>
        <button @click="open_users()" class="category">Users</button>
        <button @click="open()" id="add">Add Product</button>
    </div>
    <section class="menu">
        <p class="col">Product</p>
        <p class="col">Description</p>
        <p class="col">Price</p>
        <p class="col">ID</p>
        <p class="col">Category</p>
        <p class="col">Actions</p>
    </section>
    <article  v-for="product in getProducts.data['hydra:member']" :key="product.id" class="colonne">
    <section class="menu">
        <p class="col">{{product.name}}</p>
        <p class="col">{{ product.description }}</p>
        <p class="col">{{ product.price }}</p>
        <p class="col">{{product.id}}</p>
        <p class="col">{{product.categories}}</p>
        <button @click="edit(product.name, product.id, product.description, product.price.toString(), product.categories.toString())" id="edit">EDIT</button>
        <button @click="delete_product(product.id)">DELETE</button>
    </section>
    </article>
    </div>
</template>

<script>
import { useProducts } from '../stores/counter.js';
import { mapActions, mapState } from "pinia";


const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNTE5MTcsImV4cCI6MTcwMDI1NTUxNywicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImFudG9pbmUubG9wZXpAZXBpdGVjaC5kaWdpdGFsIn0.G3dzMHZkxX08gyIse3u8MBsqAMMeBLfAXEwP-lPspfCGinlgEbafbXuXcDRRAuGRe5l-4Op1HSPQg7BhrykWy93jWAiT6VPnnwpOhY82DrGRlOQxjOWC1mbYhkJ5QRZBJa4719OchrwrhxJNPmMped8au2nreVz7vih9sCcxxMNXvdN551THrNSQSuD2Ml0qfHywIEcy0V1IIjDFSYJ9hVaYVAQHO5qDq57UKqafaLGo2YIpmQVL4tRseaVjZyPkGPTDwRj6usMLq6iqktfWI7uPcAprd9BAfnX_ax2ap34SLFgl1pwfDnNkR7ZnFeK98cW0G2xM_pcCp3EqFiTQ4Q';

export default {
    data() {
        return {
            products: []
        };
    },
    async mounted() {
        await this.fetchProduct;
    },
    computed: {
        ...mapActions(useProducts, ["fetchProduct"]),
        ...mapState(useProducts, ["getProducts"]),
    },
    methods: {
        headers: {
            'Authorization': `Bearer ${token}`,
            'Content-Type': 'application/json'
        },
            async delete_product(id) {
                try {
                    const response = await fetch(`http://localhost/api/products/${id}`, {
                        method: 'DELETE',
                        headers: {
                            'Authorization': `Bearer ${token}`,
                            'Content-Type': 'application/json',
                        },
                    });
                    if (!response.ok) {
                        throw new Error(`Request failed with status ${response.status}`);
                    }
                    location.reload();
                } catch (error) {
                    console.error('Error deleting product:', error.message);
                }
            },
            open_users() {
            const url_window = 'http://localhost:5173/users';
            window.open(url_window, '_blank');
            },
            open_categories() {
            const url_window = 'http://localhost:5173/categories';
            window.open(url_window, '_blank');
            },
            open() {
            const url_window = 'http://localhost:5173/add';
            window.open(url_window, '_blank');
            },
            open_admin() {
            const url_window = 'http://localhost:5173/admin';
            window.open(url_window, '_blank');
            },
            edit(aname, id, description, price, categorie) {
                this.$router.push({
                    name: "edit",
                    params: {
                        "name": aname,
                        "id": id,
                        "description": description,
                        "price": price,
                        "categories": categorie,
                }
            })
        }
    }
}
</script>
<!-- FIN HTML -->


<!-- FIN JS -->

<style>

.button {
    padding-top: 100px;
    padding-left: 35%;
}
.category {
    padding: 50px
}
#add {
    border: solid 1px rgb(0, 191, 255);
    color: rgb(0, 191, 255);
    background-color: white;
}
.menu {
    display: flex;
    padding-top: 40px;
}

.col {
    width: 200px;
    border: solid 1px black;
}
</style>

<!-- FIN CSS -->