<template>
    <ion-header>
        <ion-toolbar>
            <ion-title>
                <div class="namePage">
                    <img style="width:50px;margin-right: 5px" alt="Vue logo" src="../assets/france.jpg"><span>{{title}}</span>
                </div>
            </ion-title>
        </ion-toolbar>
    </ion-header>
</template>
<script>
    export default {
        name : "Header",
        props: {
            title : String
        }
    }
</script>
<style>
    .namePage{
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>