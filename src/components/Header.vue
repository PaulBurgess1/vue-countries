<template>
<div class="header-container row gx-0">
    <div class="header-title">
        <h1 class="header-title">
            <i class="far fa-flag"></i>
            Country Information
            <i class="far fa-flag"></i>
        </h1>
    </div>
    
</div>
</template>


<script>
export default {
}
</script>

<style>
.header-container{
    display: flex;
    justify-content: center;
    align-items: center;
    text-align:center;
    background-color: var(--clr-bg-hf);
    color: var(--clr-text);
    padding-top:1rem;
    padding-bottom: 1rem;
}
h1{
    color: var(--clr-text);
}
.header-title{
    color: var(--clr-text);
}
.header-title > i{
    color: var(--clr-text);
}
</style>