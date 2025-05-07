<script>
  import Footer from "../components/Footer.svelte";
  import Header from "../components/Header.svelte";
  import "../app.css";
  let y;
  let innerWidth = 0;
  let innerHeight = 0;

  function goTop() {
    document.body.scrollIntoView();
  }

  // export let title = "Luís Neto - Software Developer"; // Default title
</script>

<div
  class="container relative flex flex-col max-w-[1400px] mx-auto w-full text-sm sm:text-base min-h-screen"
>
  <div
    class={"fixed right-0 bottom-0 duration-200 flex p-10 z-[10]" +
      (y > 0
        ? " opacity-full pointer-events-auto"
        : " pointer-events-none opacity-0")}
  >
    <button
      on:click={goTop}
      class="ml-auto rounded-full bg-slate-900 text-violet-400 px-3 sm:px-3.5 hover:bg-violet-700 hover:text-white cursor-pointer aspect-square grid place-items-center hover:scale-110 transform duration-300 hover:shadow-[0_0_8px_rgba(139,92,246,0.1)] hover:shadow-violet-500"
    >
      <i class="fa-solid fa-arrow-up" />
    </button>
  </div>
  <Header {y} />
  <slot />
  <Footer />
</div>
<svelte:window bind:scrollY={y} bind:innerHeight bind:innerWidth />
