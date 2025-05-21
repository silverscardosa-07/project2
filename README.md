# New Project 

This project was created from local system.
Created by Bipasha Chatterjee..

# Simon Says Game

let gameSeq=[];
let userSeq=[];

let btns = ["red", "purple", "green", "yellow"];

let started=false;
let level=0;
let highestscore=0;

let h2 = document.querySelector("h2");

document.addEventListener("keydown", function(event) {
    if(started==false){
        console.log("Game started");
        started=true;
        levelUp();
    }
});


function levelUp(){
    userSeq=[];
    level++;
    h2.innerText= `Level ${level}`;

    let randIdx = Math.floor(Math.random()*3);
    let randColor = btns[randIdx];
    let randBtn= document.querySelector(`.${randColor}`);
    gameSeq.push(randColor);
    console.log(gameSeq);
    gameFlash(randBtn);
    
    highestscore = Math.max(level, highestscore);
 }

function gameFlash(btn){
    btn.classList.add("flash");
    setTimeout(function(){
        btn.classList.remove("flash");
    }, 250)};

function userFlash(btn){
        btn.classList.add("userflash");
        setTimeout(function(){
            btn.classList.remove("userflash");
        }, 250)};

function checkAns(idx){
    if(userSeq[idx]===gameSeq[idx]){
    if (userSeq.length === gameSeq.length){
    setTimeout(levelUp, 1000);
    }
   } else{ 
    h2.innerHTML= `Game Over! Your score was <b>${level}</b><br>HIGHEST SCORE - ${highestscore}<br> Press Any Key to Start`;
    document.querySelector("body").style.backgroundColor= "red";
    setTimeout(function(){
        document.querySelector("body").style.backgroundColor= "white";
    }, 180);
    reset();
   }
} 

function btnPress(){
   let btn= this
   userFlash(btn);

   userColor = btn.getAttribute("id");
   userSeq.push(userColor);

   checkAns(userSeq.length-1);
}

let allBtns = document.querySelectorAll(".btn");
allBtns.forEach(function(btn){
    btn.addEventListener("click", btnPress);
});

function reset(){
    gameSeq=[];
    userSeq=[];
    level=0;
    started=false;
}
