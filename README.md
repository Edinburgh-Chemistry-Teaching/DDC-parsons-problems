# Hosting Parsons on Github Template

This repository contains a selection of Parson's Problems used for teaching data-driven chemistry. The template is based on the [Codio Parsons Problems Template](https://github.com/codio-content/hosting-parsons-on-github-template) but with some specific modifications to work with Jupyter Notebooks.


## How to Add Generated Parson's Problems

1. Use [Codio's graphical Parson's problems generator](https://codio.github.io/parsons-puzzle-ui/dist/) to create a Parson's problem
2. Click EXPORT in the top left of the online generator and copy the code
3. Create a new file in this repository (e.g. `my-problem.md`)
4. At the top of the new file, add the following front matter (customising the title and permalink as appropriate):
   ``` markdown
   ---
   layout: plain
   title: My Problem Title
   permalink: /my-problem/
   ---
   ```
4. Paste the Parson's problem code into the new file
5. If you want to include a feedback box on the problem page, modify the following code 
    ``` html
    <p> 
        <input id="feedbackLink" value="Get Feedback" type="button" /> 
        <input id="newInstanceLink" value="Reset Problem" type="button" /> 
    </p>

    <script type="text/javascript"> 

    .... MORE CODE ....

    $("#feedbackLink").click(function(event){ 
    event.preventDefault(); 
    parsonsPuzzle.getFeedback(); 
    ```

    into this:

    ``` html
    <p> 
        <input id="feedbackLink" value="Get Feedback" type="button" /> 
        <input id="newInstanceLink" value="Reset Problem" type="button" /> 
    </p>
    <fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="feedback">
    <script type="text/javascript"> 

    .... MORE CODE ....

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
    ```
6. Add a link to the new problem in `index.markdown` (customising the link text and URL as appropriate):
   ``` markdown
   - [My Problem Title](/my-problem/)
   ```
7. Commit and push your changes to GitHub. GitHub pages should automatically build the site and your new problem should be available at `https://<your-github-username>.github.io/DDC-parsons-problems/my-problem/`