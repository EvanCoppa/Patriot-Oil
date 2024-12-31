<script>
  let menuOpen = false;
  var prevScrollY;
  var mobileMenu;
  let isTransparent = true;

  document.body.addEventListener("click", (event) => {
    // console.log(event.target);
    if (menuOpen) {
      if (!event.target.closest("header")) {
        console.log("Clicked outside");
        toggleMenu();
      }
    }
  });

  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  import { onMount } from "svelte";

  let scrollPercentage = 0;

  function updateScroll() {
    const scrollY = window.scrollY;
    const totalHeight = document.body.scrollHeight - window.innerHeight;
    scrollPercentage = (scrollY / totalHeight) * 100;

    if (scrollY > prevScrollY) {
      // Scrolling down
      // document.querySelector("header").style.top = "-64px";
    } else {
      // Scrolling up
      // document.querySelector("header").style.top = "0";
    }
    if (window.location.pathname === "/") {
      if (scrollY > 1) {
        isTransparent = false;

        document.querySelector("header").style.backgroundColor = "#ffffff";
        document.getElementById("progress-container").style.opacity = 1;
         let ancors =  document.querySelector("header").getElementsByTagName("a")
        console.log(ancors.length)
        for (let i = 0; i < ancors.length - 6; i++) {
          ancors[i].style.color = "#6b7280";
        }
      } else {
        isTransparent = true;

        document.querySelector("header").style.backgroundColor = "transparent";
        document.getElementById("progress-container").style.opacity = 0;

        let ancors =  document.querySelector("header").getElementsByTagName("a")
        for (let i = 0; i < ancors.length; i++) {
          ancors[i].style.color = "#ffffff";
        }
      }
      prevScrollY = scrollY;

    }



  }

  onMount(() => {
    mobileMenu = document.querySelector(".mobile-menu");
    console.log(window.location)
    prevScrollY = window.scrollY;
    window.addEventListener("scroll", updateScroll);
    if(window.location.pathname != "/"){
      document.querySelector("header").style.backgroundColor = "#ffffff";
      document.getElementById("progress-container").style.opacity = 1;
      let ancors =  document.querySelector("header").getElementsByTagName("a")
      for (let i = 0; i < ancors.length; i++) {
        ancors[i].style.color = "#6b7280";
      }
    }

    return () => {
      window.removeEventListener("scroll", updateScroll);
    };
  });

</script>

<header class="fixed w-screen top-0 z-50 bg-white bg-opacity-20">
  <div class="mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex h-16 items-center justify-between">
      <div class="md:flex md:items-center md:gap-12">
        <a class="block text-[#C2262C]" href="/">
          {#if isTransparent == true && window.location.pathname == "/"}
           <img src="/logo-white.png" alt="Summit Exteriors Logo" class="w-[45px]" />
            
       {:else}
          <img src="/logo.png" alt="Summit Exteriors Logo" class="w-[45px]" />
      {/if}        
    </a>
       </div>

      <div class="hidden md:block">
        <nav aria-label="Global">
          <ul class="flex items-center gap-6 text-sm">
            <li>
              <a
                class=" transition-all duration-500 text-white text-base  font-medium hover:text-[#C2262C]/75 "
                href="/"
              >
                Home
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white  text-base  font-medium hover:text-[#C2262C]/75"
                href="/faq" 
              >
                Questions
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white text-base  font-medium hover:text-[#C2262C]/75"
                href="/services"
              >
                Services
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white text-base  font-medium  hover:text-[#C2262C]/75"
                href="/articles"
              >
                Articles
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white  text-base  font-medium hover:text-[#C2262C]/75"
                href="/testimonials"
              >
                Testimonials
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white text-base  font-medium hover:text-[#C2262C]/75"
                href="/about"
              >
                About
              </a>
            </li>

            <li>
              <a
                class=" transition-all duration-500 text-white  text-base  font-medium hover:text-[#C2262C]/75"
                href="/contact"
              >
                Contact
              </a>
            </li>
          </ul>
        </nav>
      </div>
      
      <div class="flex items-center gap-4">
        <div class="sm:flex sm:gap-4">
          <div onclick="window.location.href='/contact'"
            class="rounded-md cursor-default bg-red-600 hover:bg-red-500 transition-all duration-200 px-5 py-2.5 text-sm font-semibold text-white shadow"
           >
            Schedule Now
        </div>
          
        </div>

        <div class="block md:hidden">
          <button
            on:click={toggleMenu}
            class="rounded bg-gray-100 p-2 text-gray-600 transition hover:text-gray-600/75"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M4 6h16M4 12h16M4 18h16"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="progress-container opacity-0 transition-all duration-500 " id="progress-container">
    <div class="progress-bar" style="width: {scrollPercentage}%"></div>
  </div>
  <div class:active={menuOpen} class="mobile-menu">
    <nav aria-label="Global">
      <ul class="flex flex-col gap-6 text-2xl m-8">
        <li>
          <a
            class="text-red-00 font-bold transition hover:text-[#C2262C]/75"
            href="/"
          >
            Home
          </a>
        </li>

        

        <li>
          <a
            class="text-red-700 font-bold transition hover:text-[#C2262C]/75"
            href="/services"
          >
            Services
          </a>
        </li>

        <li>
          <a
            class="text-red-700 font-bold transition hover:text-[#C2262C]/75"
            href="/articles"
          >
            Articles
          </a>
        </li>
        <li>
          <a
            class="text-red-700 font-bold transition hover:text-[#C2262C]/75"
            href="/testimonials"
          >
            Testimonials
          </a>
        </li>

        <li>
          <a
            class="text-red-700 font-bold transition hover:text-[#C2262C]/75"
            href="/about"
          >
            About
          </a>
        </li>

        <li>
          <a
            class="text-red-700 font-bold transition hover:text-[#C2262C]/75"
            href="/contact"
          >
            Contact
          </a>
        </li>
      </ul>
    </nav>
  </div>
</header>

<style>
  .mobile-menu {
    position: fixed;
    top: 0;
    left: -100%; /* Change from 'right' to 'left' */
    width: 75vw;
    height: 100%;
    background: white;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1); /* Adjust shadow direction */
    transition: left 0.3s ease; /* Change 'right' to 'left' */
    z-index: 1000;
  }

  .mobile-menu.active {
    left: 0; /* Slide in from the left */
  }

  .progress-container {
    width: 100%;
    height: 2.5px; /* Adjust the height of the progress bar */
    background: rgba(0, 0, 0, 0.1);
    z-index: 1000;
  }

  .progress-bar {
    height: 100%;
    background: #c2262c; /* The color of the progress bar */
    transition: width 0.25s ease;
  }
</style>
