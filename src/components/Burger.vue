<template>
    <div class="burger">
        <svg
            :width="editor.width"
            :height="editor.gap * 2 + editor.strokeWidth"
            :viewBox="
                '0 0 ' +
                editor.width +
                ' ' +
                (editor.gap * 2 + editor.strokeWidth)
            "
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
        >
            <line
                :x1="getX()"
                :y1="editor.strokeWidth / 2.0"
                :x2="getWidth()"
                :y2="editor.strokeWidth / 2.0"
                :stroke="editor.strokeColor"
                :stroke-width="editor.strokeWidth"
                :stroke-linecap="editor.rounded ? 'round' : undefined"
            />
            <line
                :x1="getX()"
                :y1="editor.strokeWidth / 2.0 + editor.gap"
                :x2="getWidth()"
                :y2="editor.strokeWidth / 2.0 + editor.gap"
                :stroke="editor.strokeColor"
                :stroke-width="editor.strokeWidth"
                :stroke-linecap="editor.rounded ? 'round' : undefined"
            />
            <line
                :x1="getX()"
                :y1="editor.strokeWidth / 2.0 + editor.gap * 2.0"
                :x2="getWidth()"
                :y2="editor.strokeWidth / 2.0 + editor.gap * 2.0"
                :stroke="editor.strokeColor"
                :stroke-width="editor.strokeWidth"
                :stroke-linecap="editor.rounded ? 'round' : undefined"
            />
        </svg>
    </div>
</template>
<style scoped>
.burger {
    border: 2px solid #212121;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    border-radius: 5px;
    align-self: center;
}
</style>
<script>
import editor from "../store/editor.js";

export default {
    name: "Burger",
    setup() {},

    data() {
        return {
            editor: editor,
        };
    },
    mounted() {
        this.updateSvgCode();
    },
    updated() {
        this.updateSvgCode();
    },
    methods: {
        getX() {
            return editor.rounded ? editor.strokeWidth / 2 : undefined;
        },
        getWidth() {
            return editor.rounded
                ? editor.width - editor.strokeWidth / 2
                : editor.width;
        },
        updateSvgCode() {
            const svg = document.querySelector("svg");
            const lines = svg.querySelectorAll("line");

            let s =
                svg.outerHTML.slice(0, svg.outerHTML.indexOf(svg.innerHTML)) +
                "\n";

            for (const line of lines) {
                s += "\t" + line.outerHTML + "\n";
            }

            editor.svgCode = s + "</svg>";
        },
    },
};
</script>