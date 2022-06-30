<script>
  const loadSlides = Promise.all([
    import("./slides/1.svelte"),
    import("./slides/2.svelte"),
    import("./slides/3.svelte"),
    import("./slides/4.svelte"),
  ]);

  import { onMount } from "svelte";
  import { fade } from "svelte/transition";
  import Button from "./Button.svelte";
  import Slide from "./Slide.svelte";
  import { currentPage } from "./stores";

  let slides = [];

  let currentSlide;

  const params = new URLSearchParams(window.location.search);
  $currentPage = params.has("page") ? parseInt(params.get("page")) : undefined;
  history.replaceState(
    { page: $currentPage },
    null,
    isNaN($currentPage) ? "/" : `/?page=${$currentPage}`
  );

  $: currentSlide = slides[$currentPage]?.default;

  $: {
    if ($currentPage !== history.state?.page) {
      history.pushState(
        { page: $currentPage },
        null,
        isNaN($currentPage) ? "/" : `?page=${$currentPage}`
      );
    }
  }

  function handleKeyUp(event) {
    if (event.key === "ArrowLeft") {
      $currentPage = Math.max(0, $currentPage - 1);
    } else if (event.key === "ArrowRight") {
      $currentPage = Math.min(slides.length - 1, $currentPage + 1);
    } else if (event.key === "ArrowUp") {
      $currentPage = undefined;
    }
  }

  onMount(async () => {
    slides = await loadSlides;
    document.addEventListener("keyup", handleKeyUp);

    return () => {
      document.removeEventListener("keyup", handleKeyUp);
    };
  });
</script>

<link rel="stylesheet" href="./style.css" />

<svelte:window on:popstate={() => ($currentPage = history.state?.page)} />

{#if slides.length > 0}
  {#if currentSlide}
    <Slide>
      {#key $currentPage}
        <div
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
        >
          <div transition:fade|local>
            <svelte:component this={currentSlide} />
          </div>
        </div>
      {/key}
    </Slide>
  {:else}
    <h1>Table of Contents</h1>
    <ul>
      {#each slides as slide, slideIndex}
        <li>
          <Button
            on:click={() => {
              $currentPage = slideIndex;
            }}>Slide {slideIndex + 1}</Button
          >
        </li>
      {/each}
    </ul>
  {/if}
{:else}
  Loading ...
{/if}
