<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <div id="menu">
        <ul>
            <li v-for="(item, itemid) in list" :key="itemid">
                <div class="select is-small">
                    <select>
                        <option v-for="(row, rowid) in item" :key="'row'+rowid">row</option>
                    </select>
                </div>
            </li>
        </ul>
    </div>
    <div id="plot"></div>
    <!--<router-view/>-->
  </div>
</template>


<script>


export default {
  data(){
    return {
        list: [
            [
                'option1',
                'option2'
            ],
            [
                'option3',
                'option4'
            ]
        ],
        opts: {
            title: "Missing Data",
            width: 1920,
            height: 600,
        //	spanGaps: true,
            series: [
            {},
            {
                label: "CPU",
                scale: "%",
                value: (u, v) => v == null ? "-" : v.toFixed(1) + "%",
                color: "red",
            },
            {
                label: "RAM",
                scale: "%",
                value: (u, v) => v == null ? "-" : v.toFixed(1) + "%",
                color: "blue",
            },
            {
                label: "TCP Out",
                scale: "calls",
                value: (u, v) => v == null ? "-" : "# " + v.toFixed(2),
                color: "green",
            }
            ],
            axes: [
            {},
            {
                scale: '%',
                values: (u, vals, space) => vals.map(v => +v.toFixed(1) + "%"),
            },
            {
                side: 1,
                scale: 'mb',
                values: (u, vals, space) => vals.map(v => "# " + +v.toFixed(2)),
                grid: {show: false},
            },
            ],
        }
    }
  },
  mounted(){
      let data = [
          [1,2,3],
          [1,2,3],
          [1,2,3],
          [1,2,3],
      ]
      let u = new uPlot.Line(this.opts, data, document.getElementById("plot"));
  }  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
