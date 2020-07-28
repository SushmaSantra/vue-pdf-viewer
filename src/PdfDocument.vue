<template>
  <div class="pdf-document">
    <pdf-page
      v-for="page in pages"
      v-bind="{page, scale}"
      :key="page.pageNumber"
    />
  </div>
</template>

<script>
import range from 'lodash/range';
import { PdfPage } from "./PdfPage";

export default {
    components: {
        'pdf-page': PdfPage
    },
    props: ['url', 'scale'],

    data() {
        return {
            pdf: undefined,
            pages: [],
        };
    },
    watch: {
        pdf(pdf) {
            this.pages = [];
            const promises = range(1, pdf.numPages).
                map(number => pdf.getPage(number));

            Promise.all(promises).
                then(pages => (this.pages = pages));
        },
    },
    created() {
        this.fetchPDF();
    },

    methods: {
        fetchPDF() {
            import('pdfjs-dist/webpack').
                then(pdfjs => pdfjs.getDocument(this.url)).
                then(pdf => (this.pdf = pdf));
        },
    },
}
</script>