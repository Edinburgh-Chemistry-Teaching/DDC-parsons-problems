---
layout: page
title: NMR Problem
permalink: /NMR-problem/
---

<div id="sortableTrash" class="sortable-code"></div> 
<div id="sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="feedbackLink" value="Get Feedback" type="button" /> 
    <input id="newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="feedback">
<script type="text/javascript"> 
(function(){
  var initial = "FOR each NMR spectrum:\n" +
    "    read in NMR data file(s)\n" +
    "    extract time from NMR file\n" +
    "    fit NMR peak of interest\n" +
    "    extract peak area\n" +
    "    convert area to concentration\n" +
    "plot concentration vs time";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#feedbackLink").click(function(event){ 
      event.preventDefault(); 
      var feedback = parsonsPuzzle.getFeedback(); 
      console.log(feedback);
  }); 
})(); 
</script>