<template>
    <div class="container">
        <div class="grid">
            <Controls class="c1" />
            <Burger class="c2" />
            <Export class="c3" />
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    gap: 5em;
}
.grid {
    display: grid;
    grid-template-columns: auto auto;
    grid-template-rows: auto auto;
    gap: 4em 4em;
    grid-template-areas: "c1 c2" ". c3";
}
.c1 {
    grid-area: c1;
}
.c2 {
    grid-area: c2;
}
.c3 {
    grid-area: c3;
}
</style>

<script>
import Burger from "./Burger.vue";
import Controls from "./Controls.vue";
import Export from "./Export.vue";

export default {
    name: "BurgerGenerator",
    components: { Controls, Burger, Export },
};
</script>
