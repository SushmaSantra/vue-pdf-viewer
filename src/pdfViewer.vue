<template>
    <div>
        <pdf-document v-bind="{url, scale}" />        
    </div>
</template>

<script>
import { PdfDocument } from "./PdfDocument.vue";
export default {
    name: 'PdfViewer',
    components: {
        'pdf-document': PdfDocument
    },
    data() {
        return {
            url: 'https://cdn.filestackcontent.com/5qOCEpKzQldoRsVatUPS', 
            scale: 2,
        }
    },
}
</script>