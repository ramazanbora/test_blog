---
layout: page
title: Real Incomes
permalink: /real-incomes/
---



<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.4/Chart.js"></script>


<canvas id="myChart" style="width:100%;max-width:700px"></canvas>

<script src="{{ site.baseurl }}/assets/some-script-2.js" type="text/javascript"></script>


{% assign row = site.data.RealIncomedata[0] %}
{{ row | inspect }}


<table>
  {% for row in site.data.RealIncomedata %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}
  {% endfor %}
</table>
