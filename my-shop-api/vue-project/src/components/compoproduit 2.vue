<template>
    <div>
      <section>
        
        <article v-for="product in products" :key="product.id">
         
          <img src=".png" alt="">
          <div class="nomprix">
            <h6>{{ product.name }}</h6>
            <p class="prix">{{ product.price }}$</p>
          </div>
          <p class="categorie">{{ product.categories }}</p>
      
          <p class="description">{{ product.description }}</p>
          <div class="etoilepanier">
            <img class="etoile" src="../components/5 étoiles.png" alt="5 étoiles">
            <img class="ajouter-au-panier" src="../components/shopping-cart-1.png" alt="Ajouter au panier">
          </div>
        </article>
      </section>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'compoproduit',
    data() {
      return {
        products: []
      };
    },
    mounted() {
      axios.get('http://localhost/api/products')
        .then(response => {
          this.products = response.data['hydra:member'];
        })
        .catch(error => {
          console.error('Erreur lors de la récupération des produits:', error);
        });
    }
  };
  </script>


 <style scoped>

 /*conteneur du shop*/
section{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(375px,1fr));
    padding-left: 5vh;
    gap: 50px;
    margin-top: 25px;

}

/*box qui contient chaque image/text/prix...*/
article{
    height:350px;
    width: 340px;
    margin-top: 50px;

}

/*l'image de l'article*/
article img {
    height: 300px;
    width: 340px;

}

/*l'image du caddie dans l'article*/
article li img {
    height: 15px;
    width: 15px;
    margin-left: 24.5vh;

}

/*nom du de l'objet*/
article h4{
    margin-left: 15px;
    margin-top: 14px;

}

/*conteneur de nom et de prix pour les mettre sur la meme ligne*/
.nomprix {
    display: flex;
    height: 40px;
    justify-content: space-between;

}

/*text prix et genre de l'objet*/
article p {
    margin-left: 15px;
    font-size: 11px;
    color: rgb(124, 124, 124);

}

/*regroupement des genres d'objet*/
.categorie{
    margin-bottom: 0px;
    width: 100px;

}

/*regroupement des prix d'objet*/
.prix {
    margin-top: 12px;
    font-size: 15px;
    color: #000000;
    font-family: "indivisible", sans-serif;
        font-weight: 400;
        font-style: normal;
        margin-left: 211px;

}



/*image des étoiles*/
.etoile {
    height: 12px;
    width: 70px;
    margin-left: 15px;
    margin-bottom: 12px;


}
.ajouter-au-panier {
    height: 38px;
    width: 38px;
    margin-left: 215px;
    margin-top: 0px;
    margin-bottom: 9px;

}

.description{
    margin-top: 10px;
}


 </style>








