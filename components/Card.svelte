<script>
    export let card_image;
    export let bg_color;


    import {onMount} from "svelte";

    let window_width = window.innerWidth;
    let card_width = window_width /4 *0.60;

    function onResize(){
        window_width = window.innerWidth;
        card_width = window_width /4;
    }

    onMount(() => {
        window_width = window.innerWidth;
        window.addEventListener("resize", onResize);
    });





</script>

<div class="card"style="--bg-color: #{bg_color}">
    <div class="img_cont">
        <img class="inner_image" src={card_image}  alt="">    
    </div>
</div>

<style>

    .inner_image {
        width: 100%;
        align-self: center;
        height: auto;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    .card {
        left: 0;
        top: -15%;
        width: 15%;
        height: 125%;
        background-color: var(--bg-color);
        border: 13px solid #FFEF00;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 41px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

    }


    @media screen and (max-width: 540px) {
        .card {
            border: 4px solid #FFEF00;
            height: 110%;
        }
    }


</style>