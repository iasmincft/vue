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
                        <input type="checkbox" class="form-check-input" v-model="isExternalLink"/>
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
                @click.prevent="pageCreated({pageTitle, pageContent})"
            >Create Page</button>
        </div>
    </form>
</template>

<script>
export default {
    props: ['pageCreated'],
    data() {
        return {
            pageTitle: ''
        }
    },
}
</script>