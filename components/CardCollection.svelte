<script>

    export let x_offset;
    export let y_offset;
    export let win_prize;

    import Card from "../components/Card.svelte";
    import emoji from "../src/images/emoji.png";
    import backpack from "../src/images/backpack.png";
    import headphones from "../src/images/headphones.png";
    import powerbank from "../src/images/powerbank.png";
    import skate from "../src/images/skate.png";
    import speker from "../src/images/speaker.png";
    import tshirt from "../src/images/tshirt.png";
    import {fade} from "svelte/transition";

    let prizes = ["powerbank", "tshirt", "backpack", "speaker", "headphones", "skate"];
    let colors = ["A4F3EF", "65E1A6", "E8C1FF"]

    function get_random_color(){
        return colors[Math.floor(Math.random() * colors.length)];
    }

    function get_random_prize(){
        return prizes[Math.floor(Math.random() * prizes.length)];
    }

    function apply_card_image(card){
        switch (card){
            case "powerbank":
                return powerbank;
            break;

            case "tshirt":
                return tshirt;
            break;

            case "backpack":
                return backpack;
            break;

            case "speaker":
                return  speker;
            break;

            case "headphones":
                return headphones;
            break;

            case "skate":
                return skate;
            break;
        }

    }



</script>

{#if win_prize == undefined}
<div class="card_collection" in:fade style="left: {x_offset}%; top:{y_offset}%">
    <Card bg_color ="FF7A00"  card_image={emoji}/>
    <Card bg_color={get_random_color()} card_image={apply_card_image(get_random_prize())}/>
    <Card bg_color ="FF7A00" card_image={emoji}/>
    <Card bg_color={get_random_color()} card_image={apply_card_image(get_random_prize())}/>
    <Card bg_color ="FF7A00" card_image={emoji}/>
</div>
{:else}
<div class="card_collection" style="left: {x_offset}%; top:{y_offset}%">
    <Card bg_color={get_random_color()} card_image={apply_card_image(get_random_prize())}/>
    <Card bg_color ="FF7A00" card_image={emoji}/>
    <Card bg_color={get_random_color()} card_image={apply_card_image(win_prize)}/>
    <Card bg_color ="FF7A00" card_image={emoji}/>
    <Card bg_color={get_random_color()} card_image={apply_card_image(get_random_prize())}/>
</div>

{/if}

<style>
    .card_collection{
        position: relative;
        top:0px;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
    }

</style>