<script lang="ts">
  import Toggle from "./toggle.svelte";
  import * as config from "$lib/config";
</script>

<nav>
  <a href="/" class="title">
    <div style="display: flex;">
      <div><b>{config.title}</b></div>
      <img width="25" height="25" alt="on-fire" src="https://fav.farm/🔥" />
    </div>
  </a>

  <ul class="links">
    <li>
      <a href="/about">About</a>
    </li>
    <!--		<li>-->
    <!--			<a href="/contact">Contact</a>-->
    <!--		</li>-->
    <li>
      <a href="/rss.xml" target="_blank">RSS</a>
    </li>
  </ul>

  <Toggle />
</nav>

<style>
    nav {
        padding-block: var(--size-7);
    }

    .links {
        margin-block: var(--size-7);
    }

    a {
        color: inherit;
        text-decoration: none;
    }

    nav {
        display: flex;
        justify-content: space-between;
    }

    .links {
        display: flex;
        gap: var(--size-7);
        margin-block: 0;
    }

    @media (max-width: 768px) {
        .links {
            gap: var(--size-3);
        }
    }
</style>
