<template>
    <div v-if="loading" class="loader-wrapper">
        <span class="loader">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </span>
    </div>
    <div v-else>
        <div class="container" v-if="posts.category === 'men\'s clothing'">
            <div class="color">
            </div>
            <div class="content">
                <div class="square">
                    <img :src="posts.image" />
                    <div class="product">
                        <h1>{{ posts.title }}</h1>
                        <div class="rating">
                            <p>{{ posts.category }}</p>
                            <div class="rate">
                                <p>{{posts.rating.rate}}/5</p>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                            </div>
                        </div>
                        <p class="descriptions">{{ posts.description }}</p>
                        <div class="productMenu">
                            <h1>${{ posts.price }}</h1>
                            <div class="buttonProduct">
                                <button class="btnBuyNow">Buy Now</button>
                                <button class="btnNext" v-on:click="fetchNext">Next Product</button>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
            <div class="white">

            </div>
        </div>
        <div class="container" v-else-if="posts.category === 'women\'s clothing'">
            <div class="color-woman">
            </div>
            <div class="content">
                <div class="square">
                    <img :src="posts.image" />
                    <div class="product">
                        <h1>{{ posts.title }}</h1>
                        <div class="rating">
                            <p>{{ posts.category }}</p>
                            <div class="rate">
                                <p>3.9/5</p>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                                <span class="dot"></span>
                            </div>
                        </div>
                        <p class="descriptions">{{ posts.description }}</p>
                        <div class="productMenu">
                            <h1>${{ posts.price }}</h1>
                            <div class="buttonProduct">
                                <button class="btnBuyNow">Buy Now</button>
                                <button class="btnNext" v-on:click="fetchNext">Next Product</button>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
            <div class="white">

            </div>
        </div>
        <div class="container" v-else>
            <div class="color-empty">
            </div>
            <div class="content">
                <div class="square-empty">
                    <!-- <img src="../assets/sad-face.png" /> -->
                    <p>This product is unavailable to show</p><br />
                    <button class="btnNext" v-on:click="fetchNext">Next Product</button>
                </div>
            </div>
            <div class="white">

            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'ProductCategory',
    data() {
        return {
            posts: [],
            idx: 0,
            loading: false
        }
    },
    methods: {
        fetchNext() {
            this.idx++;
            this.loading = true
            fetch("https://fakestoreapi.com/products/" + this.idx)
                .then(response => response.json())
                .then(data => this.posts = data)
                .finally(() => (this.loading = false))
            if (this.idx === 20) {
                this.idx = 0;
            }
        },
    },
    mounted() {
        this.fetchNext();
    }

}
</script>

<style>
:root {
    --blue: #002772;
    --purple: #720060;
    --black: #1E1E1E;
    --pink: #FDE2FF;
    --bluelight: #D6E6FF;
    --grey: #3F3F3F;
    --whiteSand: #DCDCDC;
    --white: #FFFFFF;

}

* {
    padding: 0px;
    margin: 0px;
    font-family: 'Inter';
}

.container {
    width: 100%;
    height: auto;
    margin: auto;
    background: white;
}

.content {
    margin: 0px;
    padding: 0px;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
}

/*white-square*/
.square {
    width: 80%;
    margin: auto;
    padding: auto;
    background-color: white;
    box-shadow: 0.6px 1px 10px var(--whiteSand);
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.square-empty {
    width: 80%;
    margin: auto;
    height: 500px;
    padding: auto;
    background-color: white;
    box-shadow: 0.6px 1px 10px var(--whiteSand);
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-image: url('../assets/sad-face.png');
    background-repeat: no-repeat;
    background-position-x: center;
}

.square-empty img {
    position: absolute;
    height: 500px;
}

.square img {
    height: 400px;
    margin-right: 10vh;
    margin-left: 10vh;
    margin-top: 5vh;
    margin-bottom: 5vh;
}

.square .product {
    width: 680px;
    padding-right: 10vh;
}

.square .product h1 {
    color: var(--blue);
    font-size: 28px;

}

.square .product .rating {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid var(--whiteSand);
    font-size: 18px;
    padding-top: 3vh;
    padding-bottom: 3vh;
}

.square .product .descriptions {
    padding-top: 4vh;
    padding-bottom: 4vh;
    font-size: 20px;
}

.rate {
    display: flex;
    align-content: center;
    justify-content: center;
}

.rate p {
    margin-right: 4px;
}

.color {
    width: 100%;
    height: 60%;
    position: absolute;
    background-color: var(--bluelight);
    background-image: url("../assets/bg-pattern.svg");
}

.color-woman {
    width: 100%;
    height: 60%;
    position: absolute;
    background-color: var(--pink);
    background-image: url("../assets/bg-pattern.svg");
}

.color-empty {
    width: 100%;
    height: 60%;
    position: absolute;
    background-color: var(--whiteSand);
    display: block;
}

.white {
    height: 50%;
    width: 100%;
}

.productMenu {
    border-top: 1px solid var(--whiteSand);
}

.productMenu h1 {
    font-size: 28px;
    color: var(--blue);
    padding-top: 16px;
    padding-bottom: 16px;
}

.buttonProduct {
    display: flex;
}

.btnBuyNow {
    background-color: var(--blue);
    color: var(--white);
    border: none;
    padding: 1vh 10vh;
    font-size: 20px;
    margin-right: 10px;
    border-radius: 4px;
    cursor: pointer;
}

.btnNext {
    border: 2px solid var(--blue);
    color: var(--blue);
    padding: 1vh 10vh;
    font-size: 20px;
    margin-right: 10px;
    border-radius: 4px;
    cursor: pointer;
    z-index: 50;
}

.rate .dot {
    margin-left: 2px;
    height: 18px;
    width: 18px;
    background-color: var(--blue);
    border-radius: 50%;
    display: inline-block;
}

/*loader */
.loader-wrapper {
    width: 80%;
    margin: auto;
    height: 500px;
    padding: auto;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.loader {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    display: block;
    margin: 15px auto;
    position: relative;
    background: var(--whiteSand);
    box-shadow: -24px 0 var(--whiteSand), 24px 0 var(--whiteSand);
    box-sizing: border-box;
    animation: shadowPulse 2s linear infinite;
}

@keyframes shadowPulse {
    33% {
        background: var(--whiteSand);
        box-shadow: -24px 0 var(--blue), 24px 0 var(--whiteSand);
    }

    66% {
        background: var(--blue);
        box-shadow: -24px 0 var(--whiteSand), 24px 0 var(--whiteSand);
    }

    100% {
        background: var(--whiteSand);
        box-shadow: -24px 0 var(--whiteSand), 24px 0 var(--blue);
    }
}
</style>