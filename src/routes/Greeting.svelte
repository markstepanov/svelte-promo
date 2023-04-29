<script>
  import logo from "../images/logo.png"
  let root
  export {root as this}
</script>

  <div bind:this={root} id="main_block">
      <div class="greeting">
      <img id="logo" alt="cheers_logo"  src={logo}>
      <br>
      <div id="smile" class="element-to-fade">
          <p>
              Где взял?<br>
              Улыбнул
              <br>
              И за<span >брал!</span>
          </p>
      </div>
      <a id="start_button"  href="#/game" class="element-to-fade">
          НАЧАТЬ
      </a>
      </div>
    </div>

<style>


    #main_block {

        background-image: url("../images/main_image.png");
        background-size: cover;
        height: 100%;
        width: 100%;
        background-repeat: no-repeat;
        background-attachment: inherit;
        background-position: center; 
        background-size: cover;
    }

    .greeting{
        padding-top: 105px;
        margin-left: 110px;
    }
    

    #smile{
        line-height: 80px;
        font-family: 'Grandis';
        font-style: normal;
        font-weight: 900;
        font-size: 120px;
        line-height: 91%;
        text-transform: uppercase;
        color: #FFFFFF;
        -webkit-text-stroke-color: #058236;;
        -webkit-text-stroke-width: 2.00px;
        opacity: 1;
    }

    #start_button {
        line-height: 80px;
        font-family: 'Grandis';
        font-style: normal;
        font-weight: 900;
        font-size: 60px;
        text-transform: uppercase;
        color: #FFFFFF;
        -webkit-text-stroke-color: #058236;;
        -webkit-text-stroke-width: 2.00px;
        border: 0;
        border-radius: 90px;
        padding: 20px;
        background-color: #FFEF00;
        text-decoration: none;
    }

    #start_button:hover {
        background-color: #f5f1c2;
    }

    @media screen and (max-width: 540px) {
        
        #logo {
            width: 100px;
            height: 100%;
            opacity: 1;
        }
        .greeting {
            margin-top: 20px;
            margin-left: 20px;
        }

        #smile{
            font-size: 50px;
        }
    }



    /* 320px — 480px: Mobile devices
481px — 768px: iPads, Tablets
769px — 1024px: Small screens, laptops
1025px — 1200px: Desktops, large screens
1201px and more —  Extra large screens, TV */
    /* @media screen and (min-width: 540px) and (max-width: 780px) {
        
        #logo {
            width: 100px;
            height: auto;
        }
        .greeting {
            margin-top: 20px;
            margin-left: 20px;
        }

        .smile{
            font-size: 50px;
        }
    } */

</style>