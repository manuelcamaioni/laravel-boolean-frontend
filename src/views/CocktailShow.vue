<script>
    import axios from 'axios';
    export default {
        name: 'CocktailShow',

        data() {
            return {
                apiUrl: 'http://127.0.0.1:8000/api/cocktails',
                cocktail: {}
            }
        },

        methods: {
            getCocktail() {
                axios.get(`${this.apiUrl}/${this.$route.params.id}`).then(response => {
                    console.log(response.data);
                    this.cocktail = response.data;
                })
                    .catch(error => console.error(error))
            }
        },

        created() {
            this.getCocktail();
        }
    }
</script>

<style lang="scss" scoped>
    
    main {
        background-color: #161616;
        height: calc(100vh - 40px);
        overflow-y: hidden;

        div.container {
            padding: 3rem;
            
            div.card-bg {
                background-image: url(https://images.pexels.com/photos/5490965/pexels-photo-5490965.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2);
                border-radius: 20px;
                background-size: 100%;
                background-position: center;
                transition: all .5s;

                &:hover {
                    background-size: 110%;
                }

                div.card {
                    background-color: rgba(0, 0, 0, 0.7);
                    background-repeat: no-repeat;
                    color: white;
                    border-radius: 20px;

                    img {
                        border-radius: 20px;
                        width: 100%;
                    }

                    div.card-info {

                        strong {
                            color: #ffda7c;
                        }

                        div.ingredients {
                        margin-bottom: 1rem;
                        }
                    }
                }
                a.goback{
                    text-decoration: none;
                    color: white;
                    border: 1px solid #ffda7c;
                    border-radius: 5px;
                    margin-left: 0.9rem;
                    padding: 0.4rem 0.4rem 0.4rem 0rem;
                    img{
                        height: 29px;
                        width: 37px;
                        margin-bottom: 0.4rem;
                    }
                }
            }
        }
    }     

</style>

<template>
    <main>
        <div class="container">
            <div class="card-bg">
                <div class="card p-5">
                    <div class="row">
                        <div class="col-6">
                            <div class="card-info p-3"> 
                                <p class="mb-4"><strong>ID:</strong> {{ cocktail.id }}</p>
                                <h1 class="mb-4"><strong>Name:</strong> {{ cocktail.name }}</h1>
                                <p class="mb-4"><strong>Category:</strong> {{ cocktail.category }}</p>
                                <p class="mb-4"><strong>Alcoholic:</strong> {{ cocktail.alcoholic }}</p>
                                <p class="mb-4"><strong>Glass:</strong> {{ cocktail.glass }}</p>
                                <p class="mb-4"><strong>Instructions:</strong> {{ cocktail.instructions }}</p>
                                <div class="ingredients">
                                    <span><strong>Ingredients: </strong></span>
                                    <span v-for="(ingredient, index) in cocktail.ingredients">{{ ingredient.name }}<span v-if="index < cocktail.ingredients.length - 1">, </span></span>
                                    <span v-if="!cocktail.ingredients.length">Empty</span>
                                </div>
                            </div>
                            <a href="/" class="goback"><img src="../images/icon.png" alt="Logo">Back to cocktails list</a>
                        </div>
                        <div class="col-6">
                            <img :src="cocktail.image" :alt="cocktail.name">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>