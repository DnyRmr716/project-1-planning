Game choice: A quiz game called "Citation Needed!" where players guess whether or not a wikipedia article is real or not
additonal info: The game will utilize weird/unusual/comedic but real wikipedia articles and articles that I made up in an attempt to throw off the player. And its up to the player to guess if the wikipedia article displayed is either real or fake. If you manage to get through 15 questions without getting 3 strikes, You Win! Get 3 strikes, and you lose!

HTML:
    Create the basic HTML structure with <html>, <head>, and <body> tags.
    In the <head>:
        Set the title to "Citation Needed!".
        Link an external CSS file named "styles.css".
        link an external Javascript file name "app.js".
    In the <body>:
        Create a <header> section:
            Add an <h1> heading with the text "Citation Needed!".
        Create a <div> with id "instructions-box" and class "overlay":
            Inside this div, create another <div> with id "instructions-content" and class "modal":
                Add a <p> tag for the instructions text.
                Add a <button> with id "close-instructions" and the text "Close".
        Create a <main> section:
            Create a <div> with id "quiz-container" and class "hidden":
                Add an <h2> with id "question-number".
                Add a <p> with id "question-text".
                Add a <button> with id "real-button" and the text "Real".
                Add a <button> with id "fake-button" and the text "Fake".
                Create a <div> with id "result-container":
                    Add a <p> with id "result-message".
                    Add a <button> with id "next-button", class "hidden", and the text "Next".
            Create a <div> with id "score-container":
                Add a <p> with id "score" and the text "Score: 0".
                Add a <p> with id "strikes" and the text "Strikes: 0".
        Create a <footer> section:
            Add a <button> with id "restart-button", class "hidden", and the text "Restart Game".
        End of the <body>
CSS:

    Add general layout and styling for elements like body, header, main, and footer.
    Use Flexbox to center content both vertically and horizontally.
    Style the instructions box:
        Apply overlay and background styles.
        Center the content using Flexbox.
    Style buttons:
        Define normal, hover, and disabled states.
    Style the text box (question container):
        Add background, padding, and border styles.
        Style the question text.
    Style the score container:
        Add background, text styling, and spacing.
    Style the restart button:
        Use a distinct color.
        Set it to be initially hidden.

data.js:

    Declare a constant variable named questions.
    Assign an array to the questions constant.
    Populate the array with 30 elements, each being an object representing a question.
    Each question object should have the following properties:
        description: A string containing the text of the question or news headline
        isReal: A boolean value (true or false) indicating whether the description is factual or fabricated.

JavaScript:

        Initialize game state:
        Set currentQuestionIndex to 0.
        Set score to 0.
        Set strikes to 0.
        Set gameOver to false.
        Shuffle the questions array or randomly select a subset.
        Store the shuffled/selected questions in availableQuestions.
        Cache DOM elements:
        Get references to the following elements using document.getElementById:
            questionNumberElement
            questionTextElement
            resultMessageElement
            realButton
            fakeButton
            nextButton
            restartButton
            instructionsBox
            quizContainer
            scoreElement
            strikesElement
        Initialization function:
        Function initializeGame():
            Set instructionsBox display to 'block'.
            Set quizContainer display to 'none'.
            Add an event listener to the 'close instructions' button to call startQuiz() when clicked.
        Start quiz function:
        Function startQuiz():
            Set instructionsBox display to 'none'.
            Set quizContainer display to 'block'.
            Call renderQuestion().
        Render question function:
        Function renderQuestion():
            Get the current question from availableQuestions using currentQuestionIndex.
            Update the content of questionNumberElement with the question number.
            Update the content of questionTextElement with the question description.
            Clear the content of resultMessageElement.
            Set nextButton display to 'none'.
            Add event listeners to realButton and fakeButton to call checkAnswer() with the corresponding boolean value (true for 'Real', false for 'Fake').
        Check answer function:
        Function checkAnswer(userAnswer):
            Get the current question from availableQuestions.
            Disable realButton and fakeButton.
            If userAnswer matches currentQuestion.isReal:
                Increment score.
                Set resultMessageElement text to 'Correct!'.
            Else:
                Increment strikes.
                Set resultMessageElement text to 'Incorrect!'.
            Update the content of scoreElement and strikesElement with the current score and strikes.
            Call checkGameOver().
            Set nextButton display to 'block'.
            Add an event listener to nextButton to call nextQuestion() when clicked.
        Next question function:
        Function nextQuestion():
            Increment currentQuestionIndex.
            If currentQuestionIndex is less than the length of availableQuestions:
                Call renderQuestion().
            Else:
                Call endGame().
        Check game over function:
        Function checkGameOver():
            If strikes is greater than or equal to 3:
                Set gameOver to true.
                Call endGame().
        End game function:
        Function endGame():
            Disable realButton, fakeButton, and nextButton.
            If gameOver is true:
                Set resultMessageElement text to 'Game Over! You got 3 strikes.'.
            Else (assuming a win condition was added):
                Set resultMessageElement text to 'You Win!'.
            Set restartButton display to 'block'.
            Add an event listener to restartButton to call restartGame() when clicked.
        Restart game function:
        Function restartGame():
            Reset currentQuestionIndex, score, strikes, and gameOver to their initial values.
            Reshuffle or reselect questions and store them in availableQuestions.
            Update the content of scoreElement, strikesElement, and resultMessageElement.
            Set restartButton display to 'none'.
            Call startQuiz().
        Initialize the game on page load:
        Add an event listener to window to call initializeGame() when the page loads.