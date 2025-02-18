<script>
  import Infotext from '../lib/components/infotext.svelte'
  import TrashRemoved from '../lib/components/trash-removed.svelte'
  import Map from '../lib/components/map.svelte'
  import Trashgraph from '../lib/components/trashGraph.svelte'
  import ChartContinents from '../lib/components/chartContinents.svelte'
  import ChartRiverOcean from '../lib/components/chartRiverOcean.svelte'
  import SystemStatus from '../lib/components/system-status.svelte'
  import { onMount } from 'svelte'
  export let data

  let showAnimation = false

  function toggleAnimation() {
    showAnimation = !showAnimation
  }
</script>

<svelte:head>
  <title>Dashboard The Ocean Cleanup</title>
</svelte:head>

<section class="main">
  <div class="container2">
    <!-- Blue line -->
    <div class="menu">
      <div class="line" />
    </div>

    <!-- Title + Searchbar -->
    <section class="header-dashboard">
      <h1>{data.dataHygraph.dashboard.title}</h1>
    </section>

    <TrashRemoved data={data.dataApi.totals} text={data.dataHygraph} />
    <TrashRemoved data={data.dataApi.totals} text={data.dataHygraph} />

    <!-- Box 3: percentage since 2013 -->
    <section class="panel box-3">
      <ChartRiverOcean {data} />
    </section>

    <!-- Box 4: percentage in 2040 -->
    <section class="panel box-4">
      <h2>Plastic removed per continent</h2>
      <ChartContinents {data} />
    </section>

    <!-- Grafiek: share swith icons -->
    <section class="panel grafiek">
      <Trashgraph {data} />
    </section>

    <section class="map">
      <Map {data} />
    </section>

    <Infotext data={data.dataHygraph.dashboard.infotext} />

    <SystemStatus {data} />

    <!-- More: table more information links -->
    <section class="panel more" />
  </div>

  <div class="back-to-top-button">
    <a
      on:click={toggleAnimation}
      href="/"
      id="scroll-top-button"
      aria-label="scroll to top">back to top</a
    >
  </div>

  <!-- WAVES -->

  <div class="waves-wrapper-container">
    <div class="waves-wrapper {showAnimation ? 'active' : ''}">
      <svg
        class="waves"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        viewBox="0 24 150 28"
        preserveAspectRatio="none"
        shape-rendering="auto"
      >
        <defs>
          <path
            id="gentle-wave"
            d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z"
          />
        </defs>
        <g class="parallax">
          <use
            xlink:href="#gentle-wave"
            x="48"
            y="0"
            fill="rgba(92, 200, 222, 0.7)"
          />
          <use
            xlink:href="#gentle-wave"
            x="48"
            y="3"
            fill="rgba(92, 200, 222, 0.5)
					"
          />
          <use
            xlink:href="#gentle-wave"
            x="48"
            y="5"
            fill="rgba(92, 200, 222, 0.3)
					"
          />
          <use xlink:href="#gentle-wave" x="48" y="7" fill="#5cc8de" />
        </g>
      </svg>
    </div>
  </div>
</section>

<style>
  /* WAVES START */

  .waves-wrapper-container {
    position: absolute;
    z-index: 100;
    /* background: red; */
    bottom: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    display: flex;
    justify-content: center;
  }

  .waves-wrapper {
    width: 100%;
    position: absolute;
    bottom: -285px;
    left: 0;
    background: #5cc8de;
    animation: none;
  }

  .waves-wrapper.active {
    animation: grow 18s linear infinite;
  }

  .waves {
    position: relative;
    width: 100%;
    bottom: 141px; /* place the waves on top of the waves-wrapper */
    margin-bottom: -7px;
    min-height: 100px;
    max-height: 150px;
  }

  /* Animation */

  .parallax > use {
    animation: move-forever 25s cubic-bezier(0.55, 0.5, 0.45, 0.5) infinite;
  }
  .parallax > use:nth-child(1) {
    animation-delay: -2s;
    animation-duration: 7s;
  }
  .parallax > use:nth-child(2) {
    animation-delay: -3s;
    animation-duration: 10s;
  }
  .parallax > use:nth-child(3) {
    animation-delay: -4s;
    animation-duration: 13s;
  }
  .parallax > use:nth-child(4) {
    animation-delay: -5s;
    animation-duration: 20s;
  }
  @keyframes move-forever {
    0% {
      transform: translate3d(-90px, 0, 0);
    }
    100% {
      transform: translate3d(85px, 0, 0);
    }
  }

  @keyframes grow {
    0% {
      height: 0%;
    }
    20% {
      height: 10%;
    }
    40% {
      height: 30%;
    }
    60% {
      height: 50%;
    }
    80% {
      height: 70%;
    }
    100% {
      height: 100%;
    }
  }
  /*Shrinking for mobile*/
  @media (max-width: 768px) {
    .waves {
      height: 40px;
      min-height: 40px;
    }
  }

  /* WAVES END */
  .back-to-top-button a {
    z-index: 999;
    z-index: 999;
    position: absolute;
    bottom: 1%;
    right: 3%;
    padding: 2rem;
    background-color: var(--lightBlue);
    color: var(--whiteColor);
    cursor: pointer;
    border-radius: 0.5rem;
  }
  /* Proxima font */
  @font-face {
    font-family: 'Proxima';
    src: url('/ProximaNovaFont.otf') format('opentype') weight('normal');
    src: url('/Proxima-Nova-Bold.otf') format('opentype') weight('bold');
  }

  /* Base */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Proxima', sans-serif;
  }

  :root {
    --darkBlue: #143653;
    --trashRemovedBackground: white;
    --lightBlue: #5cc8de;
    --whiteColor: #ffffff;
    --lightGray: #f7f7f7;
    --accentGray: rgb(228, 228, 228);
    --textColor: #143653;
    --boxShadow: rgba(128, 128, 128, 0.132);
    --color: rgb(212, 212, 212);
    --textSize: 1.2rem;
    --iconSize: 2rem;
  }

  /* Als darkmode de standaard instelling is */
  @media (prefers-color-scheme: dark) {
    :root {
      --darkBlue: #ffffff;
      --trashRemovedBackground: #143653;
      --lightBlue: #5cc8de;
      --whiteColor: #143653;
      --lightGray: #0d2437;
      --accentGray: rgb(228, 228, 228);
      --textColor: #ffffff;
      --boxShadow: rgba(128, 128, 128, 0);
      --color: rgb(212, 212, 212);
      --textSize: 1.2rem;
      --iconSize: 2rem;
    }
  }

  :global(html) {
    font-size: 62.5%;
    scroll-behavior: smooth;
  }

  :global(body) {
    background-color: var(--lightGray);
    color: var(--textColor);
    position: relative;
  }

  h2 {
    line-height: 1.2;
    font-weight: 500;
    color: var(--darkBlue);
    margin-bottom: 1rem;
  }

  a {
    text-decoration: none;
  }

  /* Grid */
  .container2 {
    margin: 8rem 1.5rem 1.5rem 1.5rem;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    /* grid-template-rows: 0.01fr 0.1fr 1fr 1fr 0.5fr 0.8fr 0.5fr 0.5fr 1fr ; */
    gap: 1.2rem;
    grid-template-areas:
      'menu menu'
      'header-dashboard header-dashboard'
      'box-1 box-2'
      'dashboard-info dashboard-info'
      'map map'
      'share share'
      'box-3 box-3'
      'box-4 box-4'
      'grafiek grafiek'
      'more more';
  }

  .panel {
    border-radius: 0.5rem;
    padding: 1.5rem;
    background-color: var(--whiteColor);
    box-shadow: var(--boxShadow) 0px 0px 8px;
    transition: 0.2s;
  }

  /* Grid areas */
  .header-dashboard {
    display: flex;
    justify-content: space-between;
    grid-area: header-dashboard;
  }

  .menu {
    grid-area: menu;
  }

  .grafiek {
    grid-area: grafiek;
  }

  .map {
    grid-area: map;
    border-radius: 0.5rem;
    padding: 0.5rem;
    background-color: var(--whiteColor);
    box-shadow: var(--boxShadow) 0px 0px 8px;
    transition: 0.2s;
  }

  .box-3 {
    grid-area: box-3;
  }

  .box-4 {
    grid-area: box-4;
  }

  .more {
    grid-area: more;
  }

  /* line */
  .line {
    height: 2px;
    width: 18%;
    background-color: var(--lightBlue);
  }

  /* dashboard H1 */
  h1 {
    line-height: 1.2;
    font-weight: 500;
    text-transform: uppercase;
    color: var(--darkBlue);
  }
  .header-dashboard h1 {
    font-size: 2rem;
  }

  /* boxes styling */
  .box-3,
  .box-4 {
    font-size: 1.6rem;
    color: var(--lightBlue);
  }

  .box-3,
  .box-4,
  h2 {
    font-size: 1.6rem;
    color: var(--darkBlue);
  }

  /* search bar */

  @keyframes progress {
    0% {
      stroke-dasharray: 0 100;
    }
  }

  @media (min-width: 700px) {
    .container2 {
      margin: 8rem 1.5rem 1.5rem 1.5rem;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      /* grid-template-rows: 0.01fr 0.1fr .5fr 1fr 1fr 1fr 1fr; */
      gap: 1.2rem;
      grid-template-areas:
        'menu menu menu menu'
        'header-dashboard header-dashboard header-dashboard header-dashboard'
        'box-1 box-1 box-2 box-2'
        'dashboard-info dashboard-info map map'
        'dashboard-info dashboard-info map map'
        'share share share share'
        'box-3 box-3 box-4 box-4'
        'grafiek grafiek grafiek more';
    }
  }

  @media (min-width: 992px) {
    .container2 {
      margin: 5rem 2rem 2rem 22.3rem;
      grid-template-columns: repeat(6, 1fr);
      /* grid-template-rows: 0.01fr 0.1fr 0.3fr 0.4fr 0.4fr 0.6fr; */
      grid-template-areas:
        'menu menu menu menu menu menu'
        'header-dashboard header-dashboard header-dashboard header-dashboard header-dashboard header-dashboard'
        'box-1 box-1 box-1 box-2 box-2 box-2'
        'dashboard-info dashboard-info map map map map'
        'share share share share share share'
        'box-3 box-3 box-3 box-4 box-4 box-4'
        'grafiek grafiek grafiek more more more';
    }
  }

  /* Breakpoints large screen */
  @media (min-width: 1200px) {
    .more {
      grid-area: more;
    }

    .panel {
      padding: 2rem;
    }

    .map {
      padding: 1.5rem;
    }

    .box-4 {
      font-size: 3rem;
    }

    .box-3 {
      font-size: 2.5rem;
    }

    .box-3,
    .box-4,
    h2 {
      font-size: 1.5rem;
    }
  }
</style>
