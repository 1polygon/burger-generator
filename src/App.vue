<template>
    <v-app>
        <v-main>
            <BurgerGenerator />
        </v-main>
    </v-app>
</template>
<style>
html,
body {
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
    background-color: #1c1c1c;
}
* {
    scrollbar-width: thin;
    scrollbar-color: auto transparent;
}
*::-webkit-scrollbar {
    width: 8px;
    height: 8px;
}
*::-webkit-scrollbar-track {
    background: transparent;
}

*::-webkit-scrollbar-thumb {
    background-color: #6f6f70;
    border-radius: 0px;
    border: none;
}
*::-webkit-scrollbar-thumb:hover {
    background-color: #6f6f70c2;
}
*::-webkit-scrollbar-thumb:active {
    background-color: #6f6f708e;
}
</style>
<script>
import BurgerGenerator from "./components/BurgerGenerator.vue";

export default {
    name: "App",
    components: {
        BurgerGenerator,
    },
};
</script>
