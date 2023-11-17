<template>
    <div>
      <section>

         <!--filter-->
         <article>
            <h6 class="filterby">FILTER BY</h6>
            <li><a href="#">Collection</a><a href="#"><img class="chevronhaut" src="../components/chevron-en-bas.png" alt="icone chapeau noir à l'envers"></a></li>
            <li><a  href="#">Color</a><a href="#"><img class="chevronmil" src="../components/chevron-en-bas.png" alt="icone chapeau noir à l'envers"></a></li>
            <li><a href="#">Category</a><a href="#"><img class="chevronbas" src="../components/chevron-en-bas.png" alt="icone chapeau noir à l'envers"></a></li>
            <p>Price Range</p>
          <div class="pricebar">
              <div class = "price_range">
                    <div class="range-slider">
                        <input type= "range" class="min-price" value="0" min="0" max="10000" step="1">
                        <input type= "range" class="max-price" value="10000" min="0" max="10000" step="1">
                      </div>
                    <div class="price-content">
                          <p id="min-value">$0</p>
                          <p id="max-value">$10,000+</p>
                      </div>
            </div>
            </div>
        </article>
        

        <article v-for="product in products" :key="product.id">
         
          <img src="../components/square.png" alt="">
          <div class="nomprix">
            <h4>{{ product.name }}</h4>
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

.price-content {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.range-slider {
  width: 100%;
  position: relative;
  margin: 15px 0 30px 0;
}

input[type="range"] {
  
  border: 0;
  width: 100%;
  position: absolute;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  border: 0;
  height: 15px;
  width: 15px;
  border-radius: 50%;
  background-image: url(img/sercle.svg);
  background-color: #fff;
  cursor: pointer;
  margin-top: -5px;
  position: relative;
  z-index: 1;
}

input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 3px;
  background: #e8e8e8;
  border-radius: 3px;
  border: none;
}



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

/*text filterby*/
.filterby {
    color: rgb(124, 124, 124);
    font-size: 13px;
    padding-bottom: 20px;
    margin-left: 0px;

}

/*image chevron du milieu et du bas*/
img.chevronmil {
    margin-left: 27.2vh;

}



img.chevronbas {
    margin-left: 25.3vh;

}

/*liste de collection color category pricerange*/
article li {
    list-style-type: none;
    text-decoration: none;
    border-bottom: 1px solid rgb(212, 212, 212);
    line-height: 50px;
    margin-bottom: 14px;

}

/*text collection color category pricerange*/
article a {
    text-decoration: none;
    list-style-type: none;
    color: #000000;

}

li.pricerange {
    list-style-type: none;
    text-decoration: none;
    border-bottom: 0px solid rgb(255, 255, 255);
    line-height: 50px;
    margin-bottom: 14px;
    
}


 </style>
 







