<script>
  import { onMount } from 'svelte';
  import { csvParse } from 'd3-dsv';
  import { scaleLinear, max } from 'd3-scale';
  import { select } from 'd3-selection';

  let data = [];

  onMount(async () => {
    // Fetch the CSV file
    const response = await fetch('count-hero-network.csv');
    const csvText = await response.text();

    // Parse CSV data
    data = csvParse(csvText, d => ({
      hero: d.hero1,
      value: +d.value
    }));

    // Render chart
    renderChart();
  });

  function renderChart() {
    const svgWidth = 500;
    const svgHeight = 300;
    const margin = { top: 20, right: 20, bottom: 30, left: 40 };
    const width = svgWidth - margin.left - margin.right;
    const height = svgHeight - margin.top - margin.bottom;

    const svg = select('.chart-container')
      .append('svg')
      .attr('width', svgWidth)
      .attr('height', svgHeight)
      .append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);

    const x = scaleLinear()
      .domain([0, max(data, d => d.value)])
      .range([0, width]);

    const y = scaleLinear()
      .domain([0, data.length])
      .range([height, 0]);

    svg.selectAll('.bar')
      .data(data)
      .enter().append('rect')
      .attr('class', 'bar')
      .attr('x', 0)
      .attr('y', (d, i) => y(i))
      .attr('width', d => x(d.value))
      .attr('height', y.bandwidth());

    svg.selectAll('.bar-label')
      .data(data)
      .enter().append('text')
      .attr('class', 'bar-label')
      .attr('x', d => x(d.value))
      .attr('y', (d, i) => y(i) + y.bandwidth() / 2)
      .attr('dx', 3) // padding-left
      .attr('dy', '.35em') // vertical-align: middle
      .text(d => d.value);
  }
</script>

<div class="chart-container"></div>

<style>
  .bar {
    fill: steelblue;
  }

  .bar-label {
    fill: white;
    font: 10px sans-serif;
  }
</style>
