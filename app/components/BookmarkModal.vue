<template>
    <div id="bookmark-modal" class="ui small modal">
        <i class="close icon"></i>
        <div class="header">
            Add a new bookmark
        </div>
        <div class="content">

            <form class="ui form">
            <div class="field">
                <label>Bookmark Title</label>
                <input v-model="bookmarkTitle" type="text" placeholder="Enter a title for your bookmark...">
            </div>
            <div class="field">
                <label>Bookmark URL</label>
                <input v-model="bookmarkUrl" type="text" placeholder="Enter the URL for your bookmark...">
            </div>
            <div class="field">
                <label>Bookmark category</label>
                <select v-model="bookmarkCategory" class="ui simple dropdown">
                <option value="">Select a category</option>
                <template v-for="(name, color) in categories">
                    <option :value="{ name }">{{ name }}</option>
                </template>
                </select>
            </div>
            </form>

        </div>
        <div class="actions">
            <div @click="addBookmark" class="ui inverted purple button">Add</div>
        </div>
    </div>
</template>

<script>
    import store from '../store'
    import Vue from 'vue'
    var eventHub = new Vue()

    export default {
        data () {
            return {
            bookmarkTitle: '',
            bookmarkUrl: '',
            bookmarkCategory: ''
            }
        },
        props: ['categories'],
        methods: {
            addBookmark () {
            const newBookmark = {
                title: this.bookmarkTitle,
                url: this.bookmarkUrl,
                category: this.bookmarkCategory
            }
            store.addBookmark(newBookmark)
            $('#bookmark-modal').modal('hide')
            }
        },
        created: function() {
            eventHub.$on('add-bookmark', function () {
                this.bookmarkTitle = this.bookmarkUrl = this.bookmarkCategory = ''
                $('#bookmark-modal').modal('show')
            })
        }
    }
</script>