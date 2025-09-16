---
layout: plain
title: Reaction Sequence
permalink: /reaction-sequence/
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
  var initial = "FOR each pair of structures:\n" +
    "    Determine (summed) distance between equivalent pairs of atoms (e.g. O-O, Br-Br etc).\n" +
    "Assign largest distance as that between start/end points\n" +
    "Use starting point as `current` step\n" +
    "LOOP continuously:\n" +
    "    Find minimum distance from current step\n" +
    "    IF not already part of sequence:\n" +
    "        Assign to sequence.\n" +
    "    IF next in sequence is the end point:\n" +
    "        STOP - problem complete.\n" +
    "    Change `current` step to next in sequence";
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
      var message = feedback.html || feedback.feedback;
      if (!message && feedback.length) {
          message = feedback.join("\n")
      }
      message = message && !feedback.success ? message: "Congratulations, you solved the problem!";

      var feedbackContainer = document.getElementById("feedback");
      feedbackContainer.innerHTML = message;
      
  }); 
})(); 
</script>