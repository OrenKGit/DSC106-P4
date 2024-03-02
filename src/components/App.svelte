<script>

  import BarChart from "./BarChart.svelte";
  import netdata from './cleaned-hero-network.json'
  import data from './count-hero-network.json'
  //console.log('data', netdata)
  //console.log('cnt', data)

</script>

<main>
  <h1><center>Six Degrees of Spiderman</center></h1>
  <h3><center>A Marvel Comics Network Graph</center></h3>  
  <h4><center>
    Which Heroes are Connected the Most?
    <br>
    50 Heroes with the most connections
  </center></h4>
  <div>
    <center><BarChart {data}/></center>
  </div>
  <h4><center>Prototype Write Up:</center></h4>
  <div>
    <center>
    <b><center>What Have We Done So Far?</center></b>
    <br>
    So far we have spent the majority of our time discussing and planning out our final visualizations.
    <br>
    We spent a lot of time finding a suitable dataset to demonstrate the sociology phenomenon that we are aiming to visualize/explain.
    <br>
    We also spent considerable time attempting to build a basic network graph visualization but haven't yet succeeded.
    <br>
    Currently we have a chart showing the most connected Marvel characters that will serve as extra information
    <br>
    provided to the reader to allow them to understand the scale of character's number of connections
    <br><br>
    <b><center>What Will Be The Most Challenging Part?</center></b>
    <br>
    The most challenging part of our project will likely be implementing the expolarability onto the already challenging network graph.
    <br>
    We have already been struggling to implement the network graph and we believe our desired final implementation will require
    <br>
    a shortest path algorithm on top of animations on the network graph.
    <br>
    We plan to allow the reader to select two heroes of their choice through a dropdown menu which will then show 
    <br>
    how these two heroes are connected to eachother through comic appearances, growing edge by edge on the graph.
    </center>
  </div>

  
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
  }

  :global(#map) {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  }

  input {
    display: inline-block;
    width: 100%;
    position: relative;
    margin: 0;
    cursor: pointer;
  }

  .overlay {
    font-size: 0.9em;
    background-color: rgba(100, 100, 100, 0.1);
    position: absolute;
    min-width:250px;
    width: 15%;
    top: 10px;
    right: 10px;
    padding: 10px;
    z-index: 3;
    font-family: sans-serif;
    font-weight: lighter;
    color: rgba(200, 200, 200, 1);
  }

  .overlay2 {
    font-size: 0.9em;
    background-color: rgba(100, 100, 100, 0.1);
    position: absolute;
    min-width:250px;
    width: 15%;
    top: 10px;
    left: 10px;
    padding: 10px;
    z-index: 3;
    font-family: sans-serif;
    font-weight: lighter;
    color: rgba(200, 200, 200, 1);
  }

  .overlay3 {
    font-size: 0.9em;
    background-color: #6464641a;
    position: absolute;
    min-width:250px;
    width: 15%;
    top: 380px;
    right: 10px;
    padding: 10px;
    z-index: 3;
    font-family: sans-serif;
    font-weight: lighter;
    color: rgba(200, 200, 200, 1);
    overflow: auto;
    max-height: 400px;
  }

  .overlay4 {
  font-size: 0.6em;
  background-color: rgba(100, 100, 100, 0.1);
  position: absolute;
  min-width: 250px;
  width: 15%;
  top: 165px;
  right: 10px;
  padding: 10px;
  z-index: 3;
  font-family: sans-serif;
  font-weight: lighter;
  color: rgba(200, 200, 200, 1);
}

  .cuisine-label {
    font-size: 2.2em
  }

  label {
    font-size: 1.5em;
    font-family: sans-serif;
    font-weight: lighter;
  }

  .label2 {
    font-size: 1em;
    font-family: sans-serif;
    font-weight: lighter;
  }
  a:link {
    color: red;
    background-color: transparent;
    text-decoration: none;
  }

  a:visited {
    color: red;
    background-color: transparent;
    text-decoration: none;
  }
  .checkboxes {
    display: flex;
    align-items: center;
    margin-bottom:5px;
  }
  .checkbox-container {
    display: grid;
    grid-template-columns: auto;
    gap: 5px;
  }
  .checkbox-label {
    display: flex;
    align-items: center;
    visibility:hidden;
  }

</style>