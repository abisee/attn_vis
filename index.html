<!--
Attention Visualizer by Abigail See, abisee@stanford.edu
Originally based on code by Andrej Karpathy described here:
  http://karpathy.github.io/2015/05/21/rnn-effectiveness/
and available here:
  http://cs.stanford.edu/people/karpathy/viscode.zip
-->

<!doctype html>
<html lang="en">
 <head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <title>Attention Visualizer</title>
  <meta name="description" content="">
  <meta name="author" content="">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="external/d3.min.js"></script>
  <script src="external/jquery-3.1.0.min.js"></script>
  <script src="external/underscore-min.js"></script>
  <script src="external/sprintf.min.js"></script>
  <link href='http://fonts.googleapis.com/css?family=Cousine' rel='stylesheet' type='text/css'>

  <style>
  #wrap {
    font-family: 'Cousine';
    position:relative;
    margin: 10px;
    font-size: 15px;
  }
  </style>
  <script>

  json_fname = "attn_vis_data.json" // file containing the text and the weights

  greenhue = 151
  yellowhue = 56

  function round(x, dp) {
    // round a float to dp decimal places
    var power_of_10 = 10**dp
    return Math.round(x*power_of_10)/power_of_10
  }

  function toColor(p, hue) {
    // converts a scalar value p in [0,1] to a HSL color code string with base color hue
    if (p<0 || p>1) {
      throw sprintf("Error: p has value %.2f but should be in [0,1]", p)
    }
    var saturation = 100 // saturation percentage
    p = 1-p // invert so p=0 is light and p=1 is dark
    var min_lightness = 50 // minimum percentage lightness, i.e. darkest possible color
    var lightness = (min_lightness + p*(100-min_lightness)) // lightness is proportional to p
    return sprintf('hsl(%d,%s%%,%s%%)', hue, saturation, lightness)
  }

  function render_art(div, data, dec_idx, dec_word) {
    // render the article. if dec_idx and dec_word are not null, we highlight the article with the attention distribution for decoder timestep dec_idx and corresponding decoder word dec_word
    var startix = 0;
    var endix = data.article_lst.length
    var attn_len = data.attn_dists[0].length
    var dec_len = data.attn_dists.length

    div.html(''); // flush
    for(var i=startix; i<endix; i++) {
      var word = data.article_lst[i]; // a string
      if (dec_idx == null) {
        var attn_wt = 0;
      } else {
        var attn_wt = data.attn_dists[dec_idx][i];
      }
      var background_color = toColor(attn_wt, yellowhue);
      var css = 'background-color:' + background_color;
      css += ';display:inline'
      var word_html = word + ' '

      // Insert "truncated here" marker to indicate how much of the original article we actually fed into the RNN
      // Note we only have attention distribution over the portion of the article before truncation
      if (i==attn_len) {
        dnew0 = div.append('div');
        dnew0.attr('class', 'd')
          .attr('style', 'color:green; font-weight:bold; text-decoration:underline; display:inline;') // apply this style
          .html('ARTICLE TRUNCATED HERE. ');
      }

      // write the sentence/word
      var dnew = div.append('div');
      dnew.attr('class', 'd')
        .attr('style', css) // apply this style
        .html(word_html)
    }
  }


  function render_dec(div, data) {
    // render the decoded summary
    var startix = 0;
    var endix = data.decoded_lst.length;

    div.html(''); // flush
    for(var i=startix; i<endix; i++) {
      var word = data.decoded_lst[i]; // a string
      css = 'display:inline;'
      if (data.hasOwnProperty('p_gens')) {
        var p_gen = data.p_gens[i];
        var background_color = toColor(p_gen, greenhue);
        css += 'background-color:' + background_color;
      } else {
        var p_gen = null;
      }
      var dnew = div.append('div');

      dnew.html(word+' ') // this is the content
        .attr('class', 'd')
        .attr('style', css) // apply this style
        // add interactivity for mouseover decoder words
        .on('mouseover', getHandleMouseOver(i, word, p_gen))
        .on('mousemove', handleMouseMove)
        .on('mouseout', handleMouseOut)
    }
  }

  function getHandleMouseOver(dec_idx, dec_word, p_gen) {
     // When you mouseover a decoder word, shows attention distribution on article
     // p_gen is null for non-pointer models
    return function() {
      // Renders the article with the appropriate highlighting
      render_art(d3.select('#art'), gdata, dec_idx, dec_word);
      // Show a tooltip giving value of p_gen
      if (p_gen != null) {
        gtooltip.text(round(p_gen, 3))
        return gtooltip.style("visibility", "visible");
      }
    }
  }

  function handleMouseMove() {
    // When you move cursor over a decoder word, tooltip shows value of generation probability for that word
    return gtooltip.style("top", (d3.event.pageY-20)+"px").style("left",(d3.event.pageX+10)+"px");
  }

  function handleMouseOut() {
    // When you move cursor away from a decoder word, stop showing generation probability tooltip
    return gtooltip.style("visibility", "hidden");
  }

  function render_abs(div,data) {
    // Show the reference abstract (summary)
    div.html(''); // flush
    var dnew = div.append('div');
    dnew.html(data.abstract_str);
  }

  function get_json_and_disp() {
    // Retrieve the json data file and display the data
    console.log("fetching " + json_fname + "...")

    function json_success(data) {
      // Displays the data
      console.log("success!")
      d3.select("#curr_datafile").html('<font color="09B509">Currently displaying: ' + json_fname + "</font>")
      gdata = data; // store globally
      render_art(d3.select("#art"), gdata, null, null);
      render_abs(d3.select("#abs"), gdata);
      render_dec(d3.select("#dec"), gdata);
    }

    function json_fail(d) {
      // Tell the user it failed to load
      console.log("failure.")
      d3.select("#curr_datafile").html('<font color="red">Failed to load ' + json_fname + "</font>")
    }

    $.getJSON(json_fname, json_success).fail(json_fail);
  }

  function start() {
    console.log("start")
    get_json_and_disp()

    // Define a tooltip that we will use to display generation probability of a decoder word when you hover over it
    var tooltip = d3.select("body")
        .append("div")
        .style("position", "absolute")
        .style("z-index", "10")
        .style("visibility", "hidden")
        .style("background", "white")
        .style("font-size", "15px")
        .style("font-family", "Cousine")
        .text("a simple tooltip");
    gtooltip = tooltip // global
  }

  </script>
  </head>
  <body onload="start();">
    <div id="wrap">
      <div id="curr_datafile">
        Current datafile name goes here.
      </div>
      <h2>Article</h2>
      <div id="art">
        article goes here
      </div>
      <h2>Reference summary</h2>
      <div id="abs">
        reference summary goes here
      </div>
      <h2>Generated summary (highlighted = high generation probability)</h2>
      <div id="dec">
        generated summary goes here
      </div>
    </div>
  </body>
</html>
