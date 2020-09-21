## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/constanzaquinteros/graphs/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/constanzaquinteros/graphs/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
<html>
  <head>

	<link rel="stylesheet" href="style.css">
	<link rel="stylesheet" href="https://simeydotme.github.io/jQuery-ui-Slider-Pips/dist/css/jqueryui.min.css">
	<link rel="stylesheet" href="https://simeydotme.github.io/jQuery-ui-Slider-Pips/dist/css/jquery-ui-slider-pips.min.css">
	<link rel="stylesheet" href="https://simeydotme.github.io/jQuery-ui-Slider-Pips/dist/css/app.min.css">

    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    
    <script type="text/javascript" src="https://simeydotme.github.io/jQuery-ui-Slider-Pips/dist/js/jquery-plus-ui.min.js"></script>
	<script type="text/javascript" src="https://simeydotme.github.io/jQuery-ui-Slider-Pips/dist/js/jquery-ui-slider-pips.js"></script>

    <script type="text/javascript">
   

   $.extend( $.ui.slider.prototype.options, { 
	    animate: 300
	});

   var ordinal = ["First","Second","Third","Fourth","Fifth","Sixth"];
   var prof = ["Native","Native-like","Very proficient","Moderate","Basic","Initial"];

   var params = {
   		order: { min: 2, max: 3 },
   		proficiency: { min: 1, max: 2 },
   		age: { min: 0, max: 60 },
   		group: "language"
   }

   function refreshParams() {
	   	params.order.min = $("#order-slider").slider("values",0);
		params.order.max = $("#order-slider").slider("values",1);

		params.proficiency.min = $("#proficiency-slider").slider("values",0);
		params.proficiency.max = $("#proficiency-slider").slider("values",1);

		params.age.min = $("#age-slider").slider("values",0);
		params.age.max = $("#age-slider").slider("values",1);

		var s = (params.order.max > params.order.min)? " to "+ordinal[params.order.max - 1]:"";
	   	s = ordinal[ params.order.min - 1 ]+s+" language";
	   	$("#order-text").text(s);

	   	s = (params.proficiency.max > params.proficiency.min)? " to "+prof[params.proficiency.max]:"";
	   	s = prof[params.proficiency.min]+s;
	   	$("#proficiency-text").text(s);

	   	s = (params.age.max > params.age.min)? " to "+params.age.max:"";
	   	s = params.age.min+s;
	   	$("#age-text").text(s);

	   	params.group = $("#group-by").val();

	   	reDraw()
   }


   $( function() {
		$("#order-slider")
	    .slider({
	        max: 6,
	        min: 1,
	        range: true,
	        values: [2,3],
	        change: refreshParams
	    }).slider("pips", { first: "pip", last: "pip" });
	   
	    $("#proficiency-slider")
	    .slider({
	        max: 5,
	        min: 1,
	        range: true,
	        values: [1,2],
	        change: refreshParams
	    }).slider("pips", { first: "pip", last: "pip" });

	     $("#age-slider")
	    .slider({
	        max: 60,
	        min: 0,
	        range: true,
	        values: [0,60],
	        change: refreshParams
	    }).slider("pips", { first: "pip", last: "pip" });
   });


      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);


      var people = [['Age','25','27','21','21','27','25','20','28','70','25','29','35','34','30','27','31','23'],
['','Spanish','Spanish','Spanish','Spanish','Russian','Spanish','English','Spanish','English','Spanish','Spanish','Spanish','Spanish','Spanish','Spanish','Spanish','Spanish'],
['','English','English','English','English','Spanish','English','French','English','French','English','English','English','English','Italian','German','English','English'],
['','French','Japanese','German','Italian','English','Portuguese','Spanish','Norwegian','Spanish','Danish','French','Italian','Polish','English','English','German','German'],
['','Italian','','Japanese','','','Amharic','','Portuguese','Japanese','','','','Italian','Finish','Mapuzungun','Portuguese','Italian'],
['','','','Latin','','','','','','Portuguese','','','','Basque','','','','French'],
['','','','Chinese','','','','','','','','','','','','','',''],
['Proficiency L2',2,2,1,1,1,1,2,2,3,1,3,2,1,2,3,1,1],
['Proficiency L3',2,4,3,2,3,3,2,4,3,3,2,3,4,2,2,3,1],
['Proficiency L4',3,'',3,'','',4,'',2,5,'','','',4,3,4,5,4],
['Proficiency L5','','',4,'','','','','',4,'','','',4,'','','',5],
['Proficiency L6','','',5,'','','','','','','','','','','','','',''],
['AoA L2','10','16','6','10','9','3','1','5','9','8','10','5','8','7','4','7','6'],
['AoA L3','18','22','16','15','6','16','26','16','20','23','16','22','28','7','10','28','15'],
['AoA L4','19','','16','','','24','','13','25','','','','32','18','18','31','2'],
['AoA L5','','','20','','','','','','60','','','','32','','','','23'],
['AoA L6','','','20','','','','','','','','','','','','','','']];

	function contar(result, people) {
		let i = 0;
		for(let p of people) {
			if(i == 0) {
				i++;
			}
			else if(p) {
				if(result[p]) {
					result[p]++;
				} else {
					result[p] = 1;
				}
			}
		}
	}

	function add(result, lang){
		if(result[lang]) {
			result[lang]++;
		} else {
			result[lang] = 1;
		}
	}

	function full_count( params ) {
		console.log(params);
		var result = {};
		for(let i = 1; i <= 6; i++) {
			if( i >= params.order.min && i <= params.order.max ) {

				let p_index = 0;
				for(let p of people[i]) {
					if(p_index > 0) {

						//PROFICIENCY
						let proficiency = (i==1)? 0 : people[i+5][p_index];
						console.log(proficiency);

						if( (params.proficiency.min == 1 || proficiency >= params.proficiency.min) && proficiency <= params.proficiency.max ) {

							//AGE
							let age = parseInt( (i==1)? 0 : people[i+10][p_index] );
							if( age >= params.age.min && age <= params.age.max ) {

								if(params.group == "language") {
									add(result, p);
								} else {
									add(result, prof[proficiency]  );
								}
							}
						}
					}
					p_index++;
				}
			}
		}

		var res = [['Idioma','Instancias']];
		for (const [key, value] of Object.entries(result)) {
			res.push([key,value]); 
		}
		return res;
	}

	let res = full_count(params);
	var chart;
	var options;
	var data;


      function drawChart() {
        data = google.visualization.arrayToDataTable(res);
        options = { title: 'Language Preference', animation: { duration: 2000, easing: 'out' }, chartArea:{top:100,width:'90%',height:'80%'} };
        chart = new google.visualization.PieChart(document.getElementById('piechart'));
        chart.draw(data, options);
      }

      function reDraw() {
      	res = full_count(params);
      	data = google.visualization.arrayToDataTable(res);
      	chart.draw(data,options);
      }

    </script>
  </head>
  <body>
    <div id="piechart" style="width: 1800px; height: 900px;"></div>
    <div id="control">
    	<table class="control" style="width: 1800px; height: 200px; font-size: 14px;">
    		<tr>
    			<td width="25%"> <b>Learning Order:</b> <span id="order-text">Second to Third languague</span> </td>
    			<td width="25%"><div id="order-slider"></div> </td>

    			<td width="25%"> <b>Proficiency:</b> <span id="proficiency-text">Native-like to Very Proficient</span>  </td>
    			<td width="25%"><div id="proficiency-slider"></div> </td>
    		</tr>
    		<tr>
    			<td width="25%"> <b>Age of Acquisition:</b> <span id="age-text">0 to 60</span> </td>
    			<td width="25%"><div id="age-slider"></div> </td>

    			<td width="25%">
    				<b>Group by:</b>
    				<select id="group-by" onchange="refreshParams()" style="width:200px;">
    					<option value="language">Language</option>
    					<option value="proficiency">Proficiency</option>
    				</select>
    			</td>
    			<td width="25%"> </td>
    		</tr>
    	</table>
    </div>


  </body>
</html>
