<script>
  import challengeList from "./data/challenge_list.json";
  import Day1 from "./components/day1/Day1.svelte";
  import Day2 from "./components/day2/Day2.svelte";
  import Day3 from "./components/day3/Day3.svelte";
  import Day4 from "./components/day4/Day4.svelte";
  import Day5 from "./components/day5/Day5.svelte";
  import Day6 from "./components/day6/Day6.svelte";
  import Day7 from "./components/day7/Day7.svelte";
  import Day8 from "./components/day8/Day8.svelte";
  import Day9 from "./components/day9/Day9.svelte";
  import Day10 from "./components/day10/Day10.svelte";
  import Day11 from "./components/day11/Day11.svelte";
  import Day12 from "./components/day12/Day12.svelte";
  import Day13 from "./components/day13/Day13.svelte";
  import Day14 from "./components/day14/Day14.svelte";
  import Day15 from "./components/day15/Day15.svelte";
  import Day16 from "./components/day16/Day16.svelte";
  import Day17 from "./components/day17/Day17.svelte";
  import Day18 from "./components/day18/Day18.svelte";
  import Day19 from "./components/day19/Day19.svelte";
  import Day20 from "./components/day20/Day20.svelte";
  import Day21 from "./components/day21/Day21.svelte";
  import Day22 from "./components/day22/Day22.svelte";
  import Day23 from "./components/day23/Day23.svelte";
  import Day24 from "./components/day24/Day24.svelte";
  import Day25 from "./components/day25/Day25.svelte";

  let containerWidth;
  $: chartWidth = containerWidth > 1200 ? 600 : containerWidth * 0.5;
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
      {#if selectedDay.day_count === 1}
        <Day1 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 2}
        <Day2 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 3}
        <Day3 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 4}
        <Day4 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 5}
        <Day5 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 6}
        <Day6 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 7}
        <Day7 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 8}
        <Day8 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 9}
        <Day9 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 10}
        <Day10 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 11}
        <Day11 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 12}
        <Day12 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 13}
        <Day13 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 14}
        <Day14 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 15}
        <Day15 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 16}
        <Day16 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 17}
        <Day17 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 18}
        <Day18 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 19}
        <Day19 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 20}
        <Day20 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 21}
        <Day21 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 22}
        <Day22 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 23}
        <Day23 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 24}
        <Day24 width={chartWidth} height={chartHeight} />
      {:else if selectedDay.day_count === 25}
        <Day25 width={chartWidth} height={chartHeight} />{/if}
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
    color: #b9b9b9;
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
    max-width: 600px;
    max-height: 600px;
    box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  }
</style>
