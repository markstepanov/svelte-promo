<script>
    import pointer from '../images/pointer.png';
    import CardCollection from "../../components/CardCollection.svelte";
    import star from "../images/Star 4.png";
    import {fly, fade} from "svelte/transition";
    import { onMount } from 'svelte';
    import { domain } from "../stores";

    let prizes = ["powerbank", "tshirt", "backpack", "speaker", "headphones", "skate"];
    
    // @ts-ignore
    const tg_ref = window.Telegram.WebApp;



    function get_random_prize(){
        return prizes[Math.floor(Math.random() * prizes.length)];
    }

    let play_button;
    let will_win = false;
    let game_state = "press_play";
    let prize = "skate";

    let r;

    onMount(async () => {
        prize = get_random_prize();
        let endpoint = domain + "/get_prize";

        try {
            let resopnce = await fetch( endpoint, {
                headers: 
                {
                    init_data: tg_ref.initData
                }
            });
            resopnce = await resopnce.json();
            r = resopnce["r"];
            console.log(resopnce)
            console.log(r);
        } catch (error){
            console.error(error);
            r = "hello";
        }
        console.log(r);
    })


    
    $: x_offset_main_col = 0;
    $: x_offset_secondary_col = -100;

    let max_spin = 0;
    if (will_win){
        max_spin = 1100;
    } else {
        max_spin = 1120;
    }


    let cur_spin = 0;

    function spin(){
        game_state = "spinning";
        cur_spin = 0;
        let rid =requestAnimationFrame(function update() {
            // console.log(cur_spin);
            // if (cur_spin >= max_spin){
            //     return;
            // }
            // else if (cur_spin > 260){
            //     x_offset_main_col +=0.5;
            //     x_offset_secondary_col+=0.5;
            //     cur_spin += 0.5;
            // }
            // else if (cur_spin > 240){
            //     x_offset_main_col +=1;
            //     x_offset_secondary_col+=1
            //     cur_spin +=1;
            // }
            // else if (cur_spin > 200){
            //     x_offset_main_col +=2;
            //     x_offset_secondary_col+=2;
            //     cur_spin+=2;
            // }
            // else if (cur_spin > 20){
            //     x_offset_main_col +=3;
            //     x_offset_secondary_col+=3;
            //     cur_spin+=3;
            // } else if (cur_spin < 20){
            //     cur_spin +=1;

            // }
            // else {
            //     x_offset_main_col +=1;
            //     x_offset_secondary_col+=1;
            // }

            cur_spin+=5;
            x_offset_main_col +=5;
            x_offset_secondary_col+=5;

            if (cur_spin >= max_spin){

                game_state = "finished";
                return;
            }
            if (x_offset_main_col > 100){
                x_offset_main_col = x_offset_main_col - 200;
            }
            else if (x_offset_secondary_col> 100){
                x_offset_secondary_col= x_offset_secondary_col- 200;
            }
            rid = requestAnimationFrame(update);
        });
    }
</script>



<div id="game_block">
    {r}
    <div id="smile" in:fade>
        <h1 id="title">П<span><img alt="the_star" id="star" src={star} ></span>дари себе улыбку :)</h1>

    </div>

    <div id="pointer" in:fade>
        <div>
            <img id="pointer_image" src={pointer} alt="pointer">
        </div>
    </div>

    <div id="carousel">
        <div class="carousel_bg">
        <CardCollection win_prize={undefined} y_offset={0} x_offset={x_offset_main_col} />
        <CardCollection win_prize={prize} y_offset={-100} x_offset={x_offset_secondary_col}/>
        </div>
    </div>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    {#if game_state == "press_play"}
    <div class="button_container" bind:this={play_button} in:fly="{{ y: 200, duration: 2000 }}" out:fade>
        <button on:click={spin} id="play_button">ЖМИ</button>
    </div>
    {:else if game_state == "finished"}
    <div transition:fly="{{y: 200, duration: 1000}}" class="button_container">
        {#if will_win}
        Поздравляем!
        {:else}
        испытай удачу <br>
        в следующий раз!
        {/if}
    </div>
    
    {/if}

</div>


<style>
    #title {
        margin: 0;
        padding: 0;
        margin-top: 30px;
    }
    #game_block{
        overflow: hidden;
    }


    #play_button{
        border-radius: 90px;
        border: 0;
        width: 300px;
        height: 100px;
        font-family: 'Grandis';
        font-style: normal;
        font-weight: 900;
        font-size: 50px;
        text-align: center;
        text-transform: uppercase;
        color: white;
        background-color: #FFEF00;
        -webkit-text-stroke-color: #058236;;
        -webkit-text-stroke-width: 2.00px;
    }
    
    .button_container {
        margin-top: 70px;
        display: flex;
        justify-content: center;
        font-family: 'Grandis';
        font-style: normal;
        font-weight: 900;
        font-size: 30px;
        text-align: center;
        text-transform: uppercase;
        color: white;
        -webkit-text-stroke-width: 2.00px;
    }

    #pointer{
        display: flex;
        justify-content: center;
    }

    #carousel {
        margin-top: 5%;
        width: 100%;
        height: 30%;
        background-color: #FFBA00;
        position: relative;
    }
    .carousel_bg{
        width: 100%;
        height: 100%;
        background-color: #FFBA00;
        position: relative;

    }




    #game_block {
        display: flex;
        flex-direction: column;
        padding: 0px;
        width: 100%;
        height: 100%;
        background: linear-gradient(117.28deg, #008A25 28.22%, #00C225 58.97%);
    }
    #smile{
        font-family: 'Grandis';
        font-style: normal;
        font-weight: 900;
        font-size: 50px;
        text-align: center;
        text-transform: uppercase;
        display: inline-block;
        color: #FFFFFF;
    }

    @media screen and (max-width: 540px) {
        
        #title {
            margin-top: 10%;

        }

        #smile{
            width: 100%;
            opacity: 1;
            font-size: 20px;
        }
        #star {
            width: 40px;
            height: auto;
        }
        #carousel {
            height: 20%;

        }
    }





</style>