---
layout: page
title: Search
permalink: /real-incomes/
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.4/Chart.js"></script>
<script src="https://www.gstatic.com/charts/loader.js"></script>
<script src="{{ site.baseurl }}/assets/some-script.js" type="text/javascript"></script>

{% assign country_details = site.data.country_details | group_by:"COUNTRY" %}
{% assign currency_iso = site.data.currency_iso | group_by:"COUNTRY" %}


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
