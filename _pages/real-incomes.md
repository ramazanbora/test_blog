---
layout: page
title: Search
permalink: /real-incomes/
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.4/Chart.js"></script>
<script src="https://www.gstatic.com/charts/loader.js"></script>
<script src="{{ site.baseurl }}/assets/some-script.js" type="text/javascript"></script>

{% assign code_working_on = "AGO" %}
{% assign country_working_on = "Angola" %}

{% assign country_details = site.data.country_details | group_by:"COUNTRY" %}
{% assign currency_iso = site.data.currency_iso | group_by:"COUNTRY" %}


{% comment %}
{{ country_details[0] }}
{{ currency_iso[0] }}
{% endcomment %}



## cool tables



{% for country in country_details %}
  {% assign country_iso = currency_iso | find: "name", country.name  %}

  <details {% if forloop.first %} open {% endif %} >
    <summary>{{ country.name }}</summary>

    - {{ country.name }} Historical Currencies

      <table>
        {% for row in country_iso.items %}
          {% if forloop.first %}
            <tr>
              {% for pair in row%}
                <th>{{ pair[0] }}</th>
              {% endfor %}
            </tr>
          {% endif %}

          {% tablerow pair in row %}
            {{ pair[1] }}
          {% endtablerow %}

        {% endfor %}
      </table>

      - {{ country.name }} Exchange Rate Progression

      {% capture exchange_rates_XR -%}
        {% for row in country.items -%}
          {{ row.XR -}}
          {{ "," -}}
        {% endfor %}
      {% endcapture %}
      {% assign exchange_rates_XR = exchange_rates_XR | pop: 1 %}

      {% capture exchange_rates_YEAR -%}
        {% for row in country.items -%}
          {{ row.YEAR -}}
          {{ "," -}}
        {% endfor %}
      {% endcapture %}

      {% assign exchange_rates_YEAR = exchange_rates_YEAR | pop: 1 %}

      <canvas id="myChart_{{ country.name }}_XR" style="width:100%;max-width:840px"></canvas>

      <script>
        createChart("myChart_{{ country.name }}_XR",[{{ exchange_rates_YEAR }}],[{{ exchange_rates_XR }}])
      </script>



          ## {{ country.name }} Population Progression

            {% capture pop -%}
              {% for row in country.items -%}
                {{ row.POPULATION -}}
                {{ "," -}}
              {% endfor %}
            {% endcapture %}
            {% assign pop = pop | pop: 1 %}

            {% capture pop_YEAR -%}
              {% for row in country.items -%}
                {{ row.YEAR -}}
                {{ "," -}}
              {% endfor %}
            {% endcapture %}

            {% assign pop_YEAR = pop_YEAR | pop: 1 %}

            <canvas id="myChart_{{ country.name }}_POP" style="width:100%;max-width:840px"></canvas>

            <script>
              createChart("myChart_{{ country.name }}_POP",[{{ pop_YEAR }}],[{{ pop }}])
            </script>




  </details>
{% endfor %}


## ayrilin

{{ currency_iso[0] }}

{% for country in currency_iso %}
  <details {% if forloop.first %} open {% endif %} >
    <summary>{{ country.name }}</summary>
    <table>
      {% for row in country.items %}
        {% if forloop.first %}
          <tr>
            {% for pair in row%}
              <th>{{ pair[0] }}</th>
            {% endfor %}
          </tr>
        {% endif %}

        {% tablerow pair in row %}
          {{ pair[1] }}
        {% endtablerow %}

      {% endfor %}
    </table>
  </details>
{% endfor %}


<table>
{% for row in currency_iso %}

  {% if forloop.first %}
  <tr>
    {% for pair in row %}
      <th>{{ pair[0] }}</th>
    {% endfor %}
  </tr>
  {% endif %}

  {% tablerow pair in row %}
    {{ pair[1] }}
  {% endtablerow %}

  {% endfor %}
</table>

{% assign currency_analysis = site.data.currency_anal | where:"CODE_WB",code_working_on  %}

{% assign code_length = currency_analysis | size %}

{% assign groups_code_wb_level = site.data.currency_anal | group_by:"CODE_WB" %}

{% comment %}
{{ groups_code_wb_level }}
{% endcomment %}
{{ groups_code_wb_level[1] }}

{{ groups_code_wb_level[1].items }}


## test 2





<table>
{% for row in currency_analysis %}



  {% if forloop.first %}
  <tr>
    {% for pair in row %}
      <th>{{ pair[0] }}</th>
    {% endfor %}
  </tr>
  {% endif %}

  {% tablerow pair in row %}
    {{ pair[1] }}
  {% endtablerow %}

  {% endfor %}
</table>






<table>
{% for row in exchange_rates %}

  {% tablerow pair in row %}
    {{ pair[1] }}
  {% endtablerow %}

{% endfor %}
</table>


{% for row in exchange_rates %}
  {{row["XR"]}}
{% endfor %}



<table>
{% for row in exchange_rates %}

  {% tablerow pair in row %}
    {{ pair[1] }}
  {% endtablerow %}

{% endfor %}
</table>

### something else

{% capture exchange_rates_XR -%}
  {% for row in exchange_rates -%}
    {{ row.XR -}}
    {{ "," -}}
  {% endfor %}
{% endcapture %}

{% comment %}
{% assign exchange_rates_XR = exchange_rates_XR | split: "," %}
{% endcomment %}
{% assign exchange_rates_XR = exchange_rates_XR | pop: 1 %}


{% capture exchange_rates_YEAR -%}
  {% for row in exchange_rates -%}
    {{ row.YEAR -}}
    {{ "," -}}
  {% endfor %}
{% endcapture %}

{% comment %}
{% assign exchange_rates_YEAR = exchange_rates_YEAR | split: "," %}
{% endcomment %}
{% assign exchange_rates_YEAR = exchange_rates_YEAR | pop: 1 %}


- size of exchange_rates_XR : {{ exchange_rates_XR | size }}
- size of exchange_rates_YEAR : {{ exchange_rates_YEAR | size }}



### Some statistics: {{ exchange_rates_YEAR | size  }}

<canvas id="myChart2" style="width:100%;max-width:840px"></canvas>

- Inspect row contents

{% assign row = exchange_rates[0] %}
{{ row | inspect }}

- create a new table

<table>
  <tr>

  </tr>

</table>

- create table header

<table>
  {% for row in exchange_rates %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

      {% tablerow pair in row %}
        {{ pair[1] }}
      {% endtablerow %}

  {% endfor %}
</table>


{% for row in exchange_rates %}
    {{ row.XR }} {{ row.COUNTRY }}
{% endfor %}




- {{ exchange_rates_XR[1] }}
- {{ exchange_rates_XR | first }}
- {{ exchange_rates_XR | last }}
- {{ exchange_rates_XR | size }}
- {{ exchange_rates_XR | last}}






{% for row in site.data.xr %}
  {{ row }}
{% endfor %}



{% assign row = site.data.code_year_analysis[0] %}

Size of data: {{ site.data.code_year_analysis | size }}


{% assign rows = site.data.xr | where:"COUNTRY","Angola"  %}


{% assign rows_xr = rows.XR %}
{{ rows }}

{{ rows_xr }}

### Look at the top row

{% assign row = site.data.code_year_analysis[0] %}
{{ row | inspect }}

### Look at the second row

{% assign row = site.data.code_year_analysis[1] %}
{{ row | inspect }}

### Look at the row country and code

{{ row["COUNTRY"] }}
{{ row["CODE_WB"] }}

### First column structured

{% assign row = site.data.code_year_analysis[0] %}
{% for pair in row %}
  {{ pair | inspect }}
  {{ pair[0] }} {{ pair[1] }}
{% endfor %}

### Find country exchange rates for Angola? Apparently returns the first row.

{% assign person = site.data.xr | find:"COUNTRY","Angola" %}
{{ person.XR }}


### Create a table for the country exchange rates for Angola

{% assign person = site.data.xr | where:"COUNTRY","Angola" %}

<table>
  {% for row in person %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>


### For Angola, list the xr rows.

{{ site.data.xr | where:"COUNTRY","Angola" }}


{% for badge in site.data.xr -%}
{% endfor %}


{% for badge in site.data.code_year_analysis %}
  {% if badge.COUNTRY == "Angola" %}
    {{ badge.CODE_WB }}
  {% endif %}
{% endfor %}



{% for badge in site.data.xr %}
{% assign person = site.data.code_year_analysis | find:"COUNTRY","Angola" %}
{{ person.XR }}
{% endfor %}

{% for badge in site.data.code_year_analysis %}
  {% if badge.COUNTRY == "Angola" %}
    {{ badge.CODE_WB }}
  {% endif %}
{% endfor %}




<table>
  {% for row in site.data.code_year_analysis %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}
  {% endfor %}
</table>



<table>
  {% for row in site.data.code_year_analysis %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>



<script>

document.write("check point 6")


var xValues = [50,60,70,80,90,100,110,120,130,140,150];
var yValues = [7,8,8,9,9,9,10,11,14,14,15];

new Chart("myChart", {
  type: "line",
  data: {
    labels: xValues,
    datasets: [{
      fill: false,
      lineTension: 0,
      backgroundColor: "rgba(0,0,255,1.0)",
      borderColor: "rgba(0,0,255,0.1)",
      data: yValues
    }]
  },
  options: {
    legend: {display: false},
    scales: {
      yAxes: [{ticks: {min: 6, max:16}}],
    }
  }
});
</script>



<div id="search-container">
    <input type="text" id="search-input" placeholder="Search through the blog posts...">
    <ul id="results-container"></ul>
</div>

<script src="{{ site.baseurl }}/assets/simple-jekyll-search.min.js" type="text/javascript"></script>

<script>
    SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    searchResultTemplate: '<div style="text-align: left !important;"><a href="{url}"><h1 style="text-align:left !important;">{title}</h1></a><span style="text-align:left !important;">{date}</span></div>',
    json: '{{ site.baseurl }}/search.json'
    });
</script>


<canvas id="myChart" style="width:100%;max-width:840px"></canvas>


<script>

document.write("check point 6")


var xValues = [50,60,70,80,90,100,110,120,130,140,150];
var yValues = [7,8,8,9,9,9,10,11,14,14,15];

new Chart("myChart", {
  type: "line",
  data: {
    labels: xValues,
    datasets: [{
      fill: false,
      lineTension: 0,
      backgroundColor: "rgba(0,0,255,1.0)",
      borderColor: "rgba(0,0,255,0.1)",
      data: yValues
    }]
  },
  options: {
    legend: {display: false},
    scales: {
      yAxes: [{ticks: {min: 6, max:16}}],
    }
  }
});
</script>



<script>

document.write("check point 6")


var xValues = [{{ exchange_rates_YEAR }}];
var yValues = [{{ exchange_rates_XR }}];

new Chart("myChart2", {
  type: "line",
  data: {
    labels: xValues,
    datasets: [{
      fill: false,
      lineTension: 0,
      backgroundColor: "rgba(0,0,255,1.0)",
      borderColor: "rgba(0,0,255,0.1)",
      data: yValues
    }]
  },
  options: {
    legend: {display: false},
    scales: {
      yAxes: [{ticks: {min: 0, max:400},}],
    }
  }
});
</script>





<script>

function createChart(chartName,xValues,yValues){

document.write("check point 6")

new Chart(chartName, {
  type: "line",
  data: {
    labels: xValues,
    datasets: [{
      fill: false,
      lineTension: 0,
      backgroundColor: "rgba(0,0,255,1.0)",
      borderColor: "rgba(0,0,255,0.1)",
      data: yValues
    }]
  },
  options: {
    legend: {display: false},
    scales: {
      yAxes: [{ticks: {min: 0, max:400},}],
    }
  }
});
}
</script>
