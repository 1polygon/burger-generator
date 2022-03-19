<template>
    <div class="export">
        <div class="row">
            <v-btn color="success" @click="copySvg">Copy SVG</v-btn>
            <v-btn color="success" @click="downloadSvg">Download SVG</v-btn>
            <v-btn color="success" @click="downloadPNG">Download PNG</v-btn>
        </div>
        <pre class="code"><code>{{ editor.svgCode }}</code></pre>
    </div>
</template>

<style scoped>
.export {
    padding: 1em;
    background-color: #212121;
    border-radius: 5px;
    max-width: 35em;
}
.row {
    display: flex;
    gap: 1em;
}
.code {
    font-family: ubuntu mono;
    margin-top: 1em;
    padding: 1em;
    color: #ffbe6a;
    background-color: #121212;
    border-radius: 5px;
    overflow: auto;
}
pre {
    white-space: pre;
}
</style>

<script>
import editor from "../store/editor";

export default {
    name: "Export",
    setup() {
        return {
            editor: editor,
        };
    },
    methods: {
        copySvg() {
            navigator.clipboard.writeText(editor.svgCode);
        },
        download(href, filename) {
            const a = document.createElement("a");
            a.style.display = "none";
            a.href = href;
            a.setAttribute("download", filename);
            document.body.appendChild(a);

            a.click();

            URL.revokeObjectURL(a.href);
            document.body.removeChild(a);
        },
        downloadSvg() {
            this.download(
                URL.createObjectURL(
                    new Blob([editor.svgCode], {
                        type: "image/svg+xml;charset=utf-8;",
                    })
                ),
                "burger.svg"
            );
        },
        downloadPNG() {
            if (!this.canvas) {
                this.canvas = document.createElement("canvas");
                this.ctx = this.canvas.getContext("2d");
            }

            this.canvas.width = editor.width;
            this.canvas.height = editor.gap * 2 + editor.strokeWidth;

            const img = new Image();
            img.src = URL.createObjectURL(
                new Blob([editor.svgCode], {
                    type: "image/svg+xml;charset=utf-8;",
                })
            );

            img.addEventListener("load", () => {
                this.ctx.drawImage(img, 0, 0);
                URL.revokeObjectURL(img.src);

                const imgUrl = this.canvas
                    .toDataURL("image/png")
                    .replace("image/png", "image/octet-stream");
                this.download(imgUrl, "burger.png");
            });
        },
    },
};
</script>