<template>
  <div class="leitura">
    <h1>Página de Leitura</h1>
    <input type="file" @change="onFileChange" accept=".pdf" />
    <canvas ref="pdfCanvas"></canvas>
  </div>
</template>

<script>
// Importa o PDF.js
import * as PDFJS from "pdfjs-dist/build/pdf";
import { GlobalWorkerOptions } from "pdfjs-dist/build/pdf";

export default {
  data() {
    return {
      file: null,
    };
  },
  created() {
    // Define o caminho para o worker do PDF.js
    GlobalWorkerOptions.workerSrc = `//cdnjs.cloudflare.com/ajax/libs/pdf.js/${PDFJS.version}/pdf.worker.min.js`;
  },
  methods: {
    onFileChange(event) {
      this.file = event.target.files[0];
      this.viewFile();
    },
    async viewFile() {
      const fileReader = new FileReader();
      fileReader.onload = async () => {
        const typedarray = new Uint8Array(fileReader.result);
        const pdf = await PDFJS.getDocument(typedarray).promise;
        const page = await pdf.getPage(1);
        const viewport = page.getViewport({ scale: 1 });

        const canvas = this.$refs.pdfCanvas;
        const context = canvas.getContext("2d");
        canvas.height = viewport.height;
        canvas.width = viewport.width;

        const renderContext = {
          canvasContext: context,
          viewport: viewport,
        };
        await page.render(renderContext).promise;
      };
      fileReader.readAsArrayBuffer(this.file);
    },
  },
};
</script>

<style scoped>
.leitura {
  padding: 20px;
}
canvas {
  border: 1px solid black;
}
</style>
