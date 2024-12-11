<script>
  import { onMount } from "svelte";
  
    const updates = [
      {
        title: "Siding Install",
        subTitle: "High Quality Siding Solutions",
        content: "Pick from our wide range of colors and options to fit any home and upgrade your exterior game to make your neighbors jealous!",
        imageUrl: "/roof_replacement.png",
      },
      {
        title: "Solar Services",
        subTitle: "Future Proof Your Home",
        content: "With a 25 year workmanship and 50 year material warranty included for free with your roof, you don't have to worry about your roof for years to come!",
        imageUrl: "/roofing.png",
      },
      {
        title: "Roof Install",
        subTitle: "Smart Roofing Solutions",
        content: "With a 25 year workmanship and 50 year material warranty included for free with your roof, you don't have to worry about your roof for years to come!",
        imageUrl: "/sandy_roof.png",
      },
      {
        title: "Gutter Install",
        subTitle: "Easy Gutter Solutions",
        content: "With a 25 year workmanship and 50 year material warranty included for free with your roof, you don't have to worry about your roof for years to come!",
        imageUrl: "/oakwood_roof.png",
      },

    ];


    let title = updates[0].title;
    let subTitle = updates[0].subTitle;
    let content = updates[0].content;
    let imageUrl = updates[0].imageUrl;
    let imageOpacity = 1;

    onMount(() => {
    let index = 0;
    const interval = setInterval(() => {
        ({ title, subTitle, content, imageUrl } = updates[index]);
        index = (index + 1) % updates.length;
    }, 3000);  

    return () => clearInterval(interval);
  });
</script>

<div class="flex lg:flex-row flex-col gap-8 m-12">
  <div class="flex flex-col lg:w-1/2  lg:m-24">
    <div class="w-full m-auto flex flex-col gap-4 lg:text-start text-center ">
      <div class="flex gap-4 ">
        <div class="h-2 w-8 bg-[#C2262C] my-auto mx-2"></div>
        <h3 class="text-neutral-600 text-xl	font-light">{subTitle}</h3>
      </div>
      <h1 class="text-5xl font-bold ">{title}</h1>
      <p class="h-24 lg:max-w-[70%] text-sm text-neutral-600">{content}</p>
      <div class="flex gap-4 lg:flex-row flex-col justify-center lg:justify-start">
        <button class="w-48 h-14 rounded-md bg-[#C2262C] lg:m-0 m-auto text-white">Schedule an Estimate</button>
        <h3 class="my-auto mx-4">or Call <a class="text-[#C2262C]" href="tel:+(585) 455-7160"> (585) 455-7160</a></h3>
      </div>
    </div>
   
  </div>
  <div class="lg:w-1/2 ">
    <img
      class="trasition-opacity duration-500 rounded-sm"
      src={imageUrl}
      style="opacity: {0 + imageOpacity}"
      alt="Summit Exteriors Roofing Rochester"
    />
  </div>
</div>

<style>
</style>




