<template>
    <div class="export">
        <div class="row">
            <v-btn color="success" @click="copySvg">Copy SVG</v-btn>
            <v-btn color="success" @click="downloadSvg">Download SVG</v-btn>
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
        downloadSvg() {
            const a = document.createElement("a");
            a.style.display = "none";
            a.href = window.URL.createObjectURL(
                new Blob([editor.svgCode], { type: "text/svg;charset=utf-8;" })
            );
            a.setAttribute("download", "burger.svg");
            document.body.appendChild(a);

            a.click();

            window.URL.revokeObjectURL(a.href);
            document.body.removeChild(a);
        },
    },
};
</script>