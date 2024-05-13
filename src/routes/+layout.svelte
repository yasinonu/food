<script lang="ts">
    import "../app.pcss";
    import { Navbar, NavBrand, NavHamburger, NavUl, NavLi } from "flowbite-svelte";
    import { page } from '$app/stores';
    $: activeUrl = $page.url.pathname;
</script>

  <Navbar>
    <NavBrand href="/">
      <img src="%sveltekit.assets%/favicon.png" class="me-3 h-6 sm:h-9" alt="Flowbite Logo" />
      <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Meal Time</span>
    </NavBrand>
    <NavHamburger/>
    <NavUl {activeUrl}>
      <NavLi href="/">Ana Sayfa</NavLi>
      <NavLi href="/profile">Profil</NavLi>
      <NavLi href="/about">Hakkında</NavLi>
    </NavUl>
  </Navbar>
<div class="px-5">
  <slot></slot>
</div>