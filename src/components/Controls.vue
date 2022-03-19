<template>
    <div class="controls">
        <div class="text-caption">Width</div>
        <v-slider
            step="1"
            max="100"
            thumb-label="always"
            tick-size="1"
            v-model="editor.width"
        ></v-slider>
        <div class="text-caption">Gap</div>
        <v-slider
            step="1"
            max="50"
            thumb-label="always"
            tick-size="1"
            v-model="editor.gap"
        ></v-slider>
        <div class="text-caption">Thickness</div>
        <v-slider
            step="1"
            max="10"
            thumb-label="always"
            tick-size="1"
            v-model="editor.strokeWidth"
        ></v-slider>
        <div class="text-caption">Rounded</div>
        <v-switch
            v-model="editor.rounded"
            color="success"
            :label="editor.rounded ? 'On' : 'Off'"
            hide-details
        ></v-switch>
    </div>
</template>
<style scoped>
.controls {
    padding: 1em;
    background-color: #212121;
    width: 15em;
    border-radius: 5px;
}
</style>
<script>
import editor from "../store/editor.js"

export default {
    name: "Controls",

    data() {
        return {
            editor: editor
        };
    },
};
</script>
