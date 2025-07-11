<template>
    
    <form action="" class="container mt-3">
        <div class="row">
            <div class="col-md-8">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Page Title
                    </label>
                    <input 
                        type="text" 
                        class="form-control"
                        v-model="pageTitle"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Content
                    </label>
                    <textarea 
                        type="text" 
                        class="form-control" 
                        rows="5"
                        v-model="pageContent"
                    ></textarea>
                </div>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link Text
                    </label>
                    <input 
                        type="text" 
                        class="form-control"
                        v-model="linkText"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link URL
                    </label>
                    <input 
                        type="text" 
                        class="form-control"
                        v-model="linkUrl"
                    />
                </div>
                <div class="row mb-3">
                    <div class ="form-check">
                        <input type="checkbox" class="form-check-input" v-model="published"/>
                        <label for="gridCheck1" class="form-check-label">
                            Published
                        </label>
                    </div>
                </div>
            </div>
        </div>
        <div class="mb-3">
            <button 
                class="btn btn-primary"
                :disabled="isFormInvalid"
                @click.prevent="submitForm"
            >Create Page</button>
        </div>
    </form>
</template>

<script>
export default {
    props: ['pageCreated'],
    computed: {
        isFormInvalid() {
            return !this.pageTitle || !this.pageContent || !this.linkText || !this.linkUrl;
        }
    },
    data() {
        return {
            pageTitle: '',
            pageContent: '',
            linkText: '',
            linkUrl: '',
            published: true
        }
    },
    methods: {
        submitForm() {
            if (!this.pageTitle || !this.pageContent || !this.linkText || !this.linkUrl) {
                alert('Please fill in all fields');
                return;
            }
            this.pageCreated({
                title: this.pageTitle,
                content: this.pageContent,
                link: {
                    text: this.linkText,
                    url: this.linkUrl
                },
                published: this.published
            });

            this.pageTitle = '';
            this.pageContent = '';
            this.linkText = '';
            this.linkUrl = '';
            this.published = true;
        }
    },
    watch: {
        pageTitle(newTitle, oldTitle) {
            if (this.linkText === oldTitle) {
                this.linkText = newTitle;
            }
        }
    }
}
</script>