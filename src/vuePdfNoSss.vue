<style src="./annotationLayer.css"></style>
<script>
    import componentFactory from './componentFactory.js'
    import pdfjsWorker from "pdfjs-dist/build/pdf.worker.entry";

    if (process.env.VUE_ENV !== 'server') {
        var pdfjsWrapper = require('./pdfjsWrapper.js').default;
        var PDFJS = require("pdfjs-dist");

        if (typeof window !== 'undefined' && 'Worker' in window && navigator.appVersion.indexOf('MSIE 10') === -1) {
            var PdfjsWorker = require('worker-loader!pdfjs-dist/build/pdf.worker.js');

            PDFJS.GlobalWorkerOptions.workerSrc = pdfjsWorker;
        }

        var component = componentFactory(pdfjsWrapper(PDFJS));
    } else {
        var component = componentFactory({});
    }

    export default component;
</script>
