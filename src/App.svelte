<script>
  import challengeList from "./data/challenge_list.json";
  import Day1 from "./components/Day1.svelte";

  let containerWidth;
  $: chartWidth = containerWidth * 0.5;
  $: chartHeight = chartWidth;

  let selectedDay = challengeList[0];
</script>

<main>
  <div class="main-content" bind:clientWidth={containerWidth}>
    <!-- Introduction -->
    <div class="description">
      <div class="introduction">
        <h1>#30DayChartChallenge 2024</h1>
        <p>
          One data visualization a day, using the promt of the
          #30DayCharChallenge (get to know the challenge).
        </p>
        <p>
          As I moved recently in the country, my theme for this year is <span
            >BRAZIL</span
          >
        </p>
      </div>

      <div class="calendar">
        <p>Select a day:</p>
        <div class="day-list">
          {#each challengeList as day}
            {#if day.available === "TRUE"}<div
                class="available"
                style="background-color: {selectedDay.day_count ===
                day.day_count
                  ? `${selectedDay.color}`
                  : ''}; color: {selectedDay.day_count === day.day_count
                  ? '#fffaf3'
                  : ''}"
                on:click={() => {
                  selectedDay = day;
                }}
                on:keydown={() => {
                  selectedDay = day;
                }}
                role="menuitem"
                tabindex={1}
              >
                {day.day_count}
              </div>
            {:else}
              <div style="color : #grey" class="unavailable">
                {day.day_count}
              </div>
            {/if}
          {/each}
        </div>
        <div
          class="selected-theme"
          style="background-color : {selectedDay.color}"
        >
          {selectedDay.theme}
        </div>
      </div>
    </div>

    <!-- Chart -->
    <div class="chart">
      <Day1 width={chartWidth} height={chartHeight} />
    </div>
  </div>
</main>

<style>
  .main-content {
    display: flex;
    gap: 50px;
    justify-content: center;
    align-items: center;
    margin: 50px 20px;
  }

  .description {
    width: 400px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  h1 {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    margin: 0px 0px;
  }

  span {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    margin: 0 auto;
    text-align: center;
  }

  p {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .day-list {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .day-list div {
    width: 8%;
    text-align: center;
    margin: 2px 7px;
    padding: 6px 0px;
    border-radius: 12px;
    font-family: "Londrina Solid", sans-serif;
    font-weight: 300;
  }

  .available {
    cursor: pointer;
  }

  .available:hover {
    background-color: #f0e8de;
  }

  .unavailable {
    color: rgb(185, 185, 185);
  }

  .selected-theme {
    color: #fffaf3;
    border-radius: 12px;
    padding: 8px 12px;
    width: fit-content;
    margin: 0 auto;
    font-family: "Londrina Solid", sans-serif;
    font-weight: 300;
  }

  .chart {
    background-color: #172527;
    max-width: 600px;
    max-height: 600px;
  }
</style>
