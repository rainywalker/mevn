<template>
    <b-row>
        <b-col cols="12">
            <h2>
                Edit Book
                <b-link href="/">(Book List)</b-link>
            </h2>
            <b-jumbotron>
                <template slot="header">
                    {{book.title}}
                </template>
                <template slot="lead">
                    ISBN: {{book.isbn}}<br>
                    Author: {{book.author}}<br>
                    Description: {{book.description}}<br>
                    Published Year: {{book.published_year}}<br>
                    Publisher: {{book.publisher}}<br>
                </template>
                <hr class="my-4">
                <p>
                    Updated Date: {{book.updated_date}}
                </p>
                <b-btn variant="success" @click.stop="editbook(book._id)">Edit</b-btn>
                <b-btn variant="danger" @click.stop="deletebook(book._id)">Delete</b-btn>
            </b-jumbotron>
        </b-col>
    </b-row>
</template>

<script>
    export default {
        name: "ShowBook",
        data () {
            return {
                book: []
            }
        },
        created () {
            this.$http.get(`/api/book/${this.$route.params.id}`)
                .then(response => {
                    this.book = response.data
                })
                .catch(e => {
                    this.errors.push(e)
                })
        },
        methods: {
            editbook (bookid) {
                this.$router.push({
                    name: 'EditBook',
                    params: { id: bookid }
                })
            },
            deletebook (bookid) {
                this.$http.delete(`/api/book/${bookid}`)
                    .then((result) => {
                        this.$router.push({
                            name: 'BookList'
                        })
                    })
                    .catch(e => {
                        this.errors.push(e)
                    })
            }
        }
    }
</script>

<style scoped>

</style>
