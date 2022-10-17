<template>
    <main>
        <h1>Post:</h1>

        <div class="posts">
            <div 
            class="card" 
            v-for="(post, index) in posts"
            :key="index"
            >
                <div 
                class="card-img"
                v-if="post.img_path"
                >
                    <img 
                    :src="post.img_path"
                    :alt="post.title"
                    >
                </div>
                <div 
                class="card-img fallback"
                v-else
                >
                    <img 
                    src="/fallback-images/posts-fallback.jpg"
                    alt="immagine segnaposto"
                    >
                </div>

                <div class="card-body">
                    <h4>
                        Titolo:
                        {{post.title}}
                    </h4>

                    <p v-if="post.category">
                        Categoria:
                        {{post.category.name}}
                    </p>
                    <p v-else>
                        Categoria: -
                    </p>
                    
                    <p v-if="post.tags.length > 0">
                        Tag:
                        <span
                        v-for="(tag, index) in post.tags"
                        :key="index"
                        >
                            {{tag.name}} |
                        </span>
                    </p>
                    <p v-else>
                        Tag: -
                    </p>

                    <p>
                        {{post.description}}    
                    </p>

                    <a href="">
                        Leggi di più
                    </a>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'AppMain',
    data() {
        return {
            posts: []
        }
    },
    methods: {
        getPosts() {
            axios.get('/api/posts')
            .then(response => {
                this.posts = response.data.result;
            })
        }
    },
    mounted() {
        this.getPosts();
    }
}
</script>

<style lang="scss" scoped>
    main {
        width: 70%;
        margin: 3rem auto;
        h1 {
            margin-bottom: 2rem;
            color: #000;
        }
        .posts {
            display: flex;
            flex-flow: row wrap;
            gap: 1rem;
            .card {
                display: flex;
                flex-direction: column;
                flex-basis: calc((100% / 3) - 1rem);
                height: 500px;
                border: 1px solid black;
                border-radius: .5rem;
                .card-img {
                    height: 50%;
                    img {
                        width: 100%;
                        height: 100%;
                        object-fit: cover;
                        object-position: center;
                    }
                }
                a {
                    text-decoration: none;
                }
            }
        }
    }
</style>