<script lang="ts">
  import Toggle from "./toggle.svelte";
  import * as config from "$lib/config";
</script>

<nav>
<!--  <a href="/" class="title">-->
<!--    {config.title}-->
<!--&lt;!&ndash;    <div style="display: flex;">&ndash;&gt;-->
<!--&lt;!&ndash;      <h4>{config.title}</h4>&ndash;&gt;-->
<!--&lt;!&ndash;      <img width="25" height="25" alt="on-fire" src="https://fav.farm/🔥" />&ndash;&gt;-->
<!--&lt;!&ndash;    </div>&ndash;&gt;-->
<!--  </a>-->

  <ul class="links">
    <li>
      <a class="home-link" href="/">
        {config.title}
        <img width="20" height="20" alt="on-fire" src="https://fav.farm/🔥" />
      </a>
    </li>
  </ul>

  <ul class="links">
    <li>
      <a href="/about">About</a>
    </li>
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

    .home-link {
        display: flex;
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
