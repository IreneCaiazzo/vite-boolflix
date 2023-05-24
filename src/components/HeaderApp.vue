<script></script>
<template>
    <header>
        <nav>
            <h1>Boolflix</h1>
            <div class="search">
                <input type="text">
                <button>Cerca</button>
            </div>
        </nav>
    </header>
</template>
<style lang="scss" scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 5rem;
    background-color: black;
    color: red;
    padding-inline: 2rem;

    input {
        margin-right: 1rem;
    }

}
</style>