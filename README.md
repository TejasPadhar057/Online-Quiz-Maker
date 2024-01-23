# Online-Quiz-Maker
HTML Code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="app">
        <h1>Simple Quiz</h1>
        <div class="quiz">
            <h2 id="question">Question goes here</h2>
            <div id="answer-buttons">
                <button class="btn">Answer 1</button>
                <button class="btn">Answer 2</button>
                <button class="btn">Answer 3</button>
                <button class="btn">Answer 4</button>
            </div>
            <button id="next-btn">Next Question</button>
        </div>

        

    </div>
    <script src="script.js"></script>
    
</body>
</html>

CSS Code
*{
    margin: 0;
    padding: 0;
    font-family: 'poppins',sans-serif;
    box-sizing: border-box;
}
body{
    background: darkorchid;
}
.app{
    background: white;
    width: 90%;
    max-width: 700px;
    margin: 100px auto;
    border-radius: 10px;
    padding: 30px;

}
.app h1{
    font-size: 35px;
    color: black;
    font-weight: 600;
    border-bottom: 1px solid black;
    padding-bottom: 30px;


}
.quiz{
    padding: 20px 0;
}
.quiz h2{
    font-size: 26px;
    color: black;
    padding-bottom: 10px;

}
.btn{
    background: white;
    color: black;
    font-size: 20px;
    width: 100%;
    border: 1px solid #222;
    padding: 10px;
    margin: 10px 0; 
    text-align: left;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.5s;
}
.btn:hover:not([disabled]){
    background: #222;
    color: white;
}
.btn:disabled{
    cursor: no-drop;
}
#next-btn{
    background: darkmagenta;
    color: white;
    font-size: 18px;
    width: 150px;
    border: 0;
    padding: 10px;
    margin: 20px auto 0;
    border-radius: 4px;
    cursor: pointer;
    display: block;
    display: none; 
}
.correct{
    background: green;
}
.incorrect{
    background: red;
}

Javascript Code
const questions =[
    {
        question: "What is the correct way to comment a single line in C++?",
        answers:[
            {text: "'// Comment text'",correct: true},
            {text: "'/* Comment text */'",correct: false},
            {text: "'-- Comment text'",correct: false},
            {text: "'# Comment text'",correct: false},

        ]
    },
    {
        question: "Which C++ keyword is used to define a class?",
        answers:[
            {text: "class",correct: true},
            {text: "struct",correct: false},
            {text: "object",correct: false},
            {text: "type ",correct: false},

        ]
    }, 
    {
        question: "Which of the following is not a valid C++ data type?",
        answers:[
            {text: "int",correct: false},
            {text: "double",correct: false},
            {text: "char",correct: false},
            {text: "real",correct: true},

        ]
    }, 
    {
        question: "What is the entry point of a Java program?",
        answers:[
            {text: "start()",correct: false},
            {text: "main()",correct: true},
            {text: "begin()",correct: false},
            {text: "init()",correct: false},

        ]
    },
    {
        question: "Which keyword is used for inheritance in Java?",
        answers:[
            {text: "inherits",correct: false},
            {text: "implements",correct: false},
            {text: "extends",correct: true},
            {text: "inherit",correct: false},

        ]
    }
];
const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex =0;
let score = 0;
 
function startQuiz(){
    currentQuestionIndex = 0;
    score = 0;
    nextButton.innerHTML = "Next";
    showQuestion();
}

function showQuestion(){
    resetState();
    let currentQuestion = questions[currentQuestionIndex];
    let questionNo = currentQuestionIndex + 1;
    questionElement.innerHTML = questionNo + ". " + currentQuestion.
    question;

    currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.text;
        button.classList.add("btn");
        answerButtons.appendChild(button);
        if(answer.correct){
            button.dataset.correct = answer.correct;
        }
        button.addEventListener("click", selectAnswer);
    });
}
 function resetState(){
    nextButton.style.display = "none";
    while(answerButtons.firstChild){
        answerButtons.removeChild(answerButtons.firstChild);
    }
 }
 function selectAnswer(e){
     const selectedBtn = e.target;
     const isCorrect = selectedBtn.dataset.correct === "true";
     if(isCorrect){
        selectedBtn.classList.add("correct");
        score++;
     }else{
        selectedBtn.classList.add("incorrect");
     }
     Array.from(answerButtons.children).forEach(button => {
        if(button.dataset.correct === "true"){
            button.classList.add("correct");
        }
        button.disabled = true;
     });
     nextButton.style.display = "block";

 }

 function showScore(){
    resetState();
    questionElement.innerHTML = `You scored ${score} out of ${questions.length}!`;
    nextButton.innerHTML = "Play Again";
    nextButton.style.display = "block"
 }

  function handleNextButton(){
    currentQuestionIndex++;
    if(currentQuestionIndex < questions.length){
        showQuestion();
    }else{
        showScore();
    }
  }

 nextButton.addEventListener("click", ()=>{
    if(currentQuestionIndex < questions.length){
        handleNextButton();
    }else{
        startQuiz();
    }
 });


startQuiz();

