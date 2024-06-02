<template>
    <div class="errorpage">
        <h2>404</h2>
        <p>Page Not Found</p>
        <p>Go to <router-link :to="`/`">Home Page</router-link></p>
    </div>
</template>

<style scoped>
.errorpage{
    width: 90%;
    height: 90%;
    max-width: 625px;
    margin: 100px auto;
    text-align: center;
    display: flex;
    flex-direction: column;
}

h2{
    font-size: 100px;
}

p{
    font-weight: bold;
}

p a{
    color: hsl(0, 0%, 100%);

    &:hover{
        color: hsl(0, 0%, 80%);
    }
}


</style>