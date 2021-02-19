<script>
  import Contact from "./Contact.svelte";
  import Products from "./Products.svelte";

  let contactUs = true;
  let openMenu = true;
  let productManage = false;
  let hamburgerBtn = "Open menu";

  // Visar contact-sidan
  function contactPage() {
    contactUs = false;
    productManage = false;
  }

  // Visar productsidan
  function productPage() {
    productManage = true;
    contactUs = true;
  }

  // Har sidebaren helt gömmd till höger
  let navWidth = 0;

  // Öppnar sidebaren, ändrar namnet på "open menu"
  const openNav = () => {
    if (openMenu == false) {
      navWidth = 40;
      openMenu = true;
      hamburgerBtn = "Close menu";
    } else if (openMenu == true) {
      navWidth = 0;
      openMenu = false;
      hamburgerBtn = "Open menu";
    }
  };

  const closeNav = () => {
    navWidth = 0;
  };
</script>

<!-- Style width {navWidth}% är Svelte-syntax. nu är navWidth sparat som en variabel -->

<div id="mySidenav" class="sidenav" style="width: {navWidth}%">
  <!-- on:click={closeNav} är svelte-syntax för att köra 
	funktionen closeNav vid klick av x-symbolen(&times;) -->
  <a href="#closer" class="closebtn" on:click={closeNav}>&times;</a>
  <a href="#1" on:click={contactPage}>Contact</a>
  <a href="#2" on:click={productPage}>Products</a>
  <a href="#3">Shopp</a>
  <a href="#4">Home</a>
</div>

<!-- on:click={openNav} är Svelte-syntax för att öppna side-naven -->
<span class="menu-btn" on:click={openNav}>{hamburgerBtn}</span>

{#if contactUs == true}
  <div id="main">
    <h1>Hello Stranger!</h1>
  </div>
{/if}

{#if contactUs == false}
  <Contact />
{/if}

{#if productManage == true}
  <Products />
{/if}

<!-- Add all page content inside this div if you want the side nav to push page content to the right (not used if you only want the sidenav to sit on top of the page -->
<style>
  .menu-btn {
    position: absolute;
    right: 5rem;
  }

  .menu-btn:hover {
    cursor: pointer;
  }
  .sidenav {
    height: 100%;
    width: 40%;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: #111;
    overflow-x: hidden;
    padding-top: 60px;
    transition: 0.5s; /* 0.5 second transition effect to slide in the sidenav */
  }

  /* The navigation menu links */
  .sidenav a {
    padding: 8px 8px 8px 32px;
    text-decoration: none;
    font-size: 25px;
    color: #818181;
    display: block;
    transition: 0.3s;
  }

  /* When you mouse over the navigation links, change their color */
  .sidenav a:hover {
    color: #f1f1f1;
  }

  /* Position and style the close button (top right corner) */
  .sidenav .closebtn {
    position: absolute;
    top: 0;
    right: 25px;
    font-size: 36px;
    margin-left: 50px;
  }

  /* Style page content - use this if you want to push the page content to the right when you open the side navigation */
  #main {
    transition: margin-left 0.5s;
    padding: 20px;
  }

  /* On smaller screens, where height is less than 450px, change the style of the sidenav (less padding and a smaller font size) */
  @media screen and (max-height: 450px) {
    .sidenav {
      padding-top: 15px;
    }
    .sidenav a {
      font-size: 18px;
    }
  }
</style>
