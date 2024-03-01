<!-- App.svelte -->
<script>
  import { onMount } from 'svelte';
  import { csvParse } from 'd3-dsv';
  import { scaleLinear, scaleBand } from 'd3-scale';
  import { max } from 'd3-array';
  import { select } from 'd3-selection';
  import { axisBottom, axisLeft } from 'd3-axis';

  let data = [];

  onMount(async () => {
    const response = await fetch('count-hero-network.csv');
    const csvData = await response.text();
    data = csvParse(csvData, d => ({
      hero: d.hero1,
      value: +d.value
    }));
    
    createChart();
  });

  function createChart() {
    const svg = select('svg');
    const margin = { top: 20, right: 20, bottom: 30, left: 40 };
    const width = +svg.attr('width') - margin.left - margin.right;
    const height = +svg.attr('height') - margin.top - margin.bottom;
    
    const x = scaleBand().rangeRound([0, width]).padding(0.1);
    const y = scaleLinear().rangeRound([height, 0]);
    
    const g = svg.append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);
    
    x.domain(data.map(d => d.hero));
    y.domain([0, max(data, d => d.value)]);
    
    g.append('g')
      .attr('class', 'axis axis-x')
      .attr('transform', `translate(0,${height})`)
      .call(axisBottom(x))
      .selectAll('text')
      .style('text-anchor', 'end')
      .attr('dx', '-.8em')
      .attr('dy', '.15em')
      .attr('transform', 'rotate(-45)');
    
    g.append('g')
      .attr('class', 'axis axis-y')
      .call(axisLeft(y).ticks(10))
      .append('text')
      .attr('transform', 'rotate(-90)')
      .attr('y', 6)
      .attr('dy', '0.71em')
      .attr('text-anchor', 'end')
      .text('Value');
    
    g.selectAll('.bar')
      .data(data)
      .enter().append('rect')
      .attr('class', 'bar')
      .attr('x', d => x(d.hero))
      .attr('y', d => y(d.value))
      .attr('width', x.bandwidth())
      .attr('height', d => height - y(d.value));
  }
</script>

<svg width="960" height="500"></svg>


<main>
  <h1>Svelte template</h1>
 
  <p>Write your HTML here</p>
</main>

<style>
  /* Write your CSS here */
</style>
