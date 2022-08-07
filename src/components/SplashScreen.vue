<template>
    <div class="splashscreen">
        <figure class="img">
            <img src="@/assets/cashflow-icon.svg" alt="Logo Cashflow">
        </figure>
        <h1><span>Cash</span>Flow</h1>
    </div>
</template>

<style scoped>
.splashscreen {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 100vh;
}

.img {
    width: 250px;
    height: 250px;
    padding: 10px;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
}

.img::before {
    border: 10px solid var(--brand-green);
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
    border-radius: 50%;
    content: "";
    display: block;
    width: 90%;
    height: 90%;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    animation: load 0.5s infinite;
}

@keyframes load {
    form {
        transform: rotate(0);
    }
    to {
        transform: rotate(360deg);
    }
}

.img img {
    width: 100%;
    height: 100%;
    object-fit: contain;
}

h1 {
    color: var(--brand-blue);
}

h1 span {
    color: var(--brand-green);
}
</style>