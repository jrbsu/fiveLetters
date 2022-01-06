var wordList = [],
    fiveLetters = [],
    wordChars = [],
    randomWordID = 0,
    chars = [],
    letterMatchesThisCycle = [],
    toColour = [],
    guess = 0,
    hits = 0,
    mostHits = 1,
    score = 500,
    randomWord = "",
    wrong = false,
    correct = false,
    letterMatches = [".", ".", ".", ".", "."],
    seconds = 0,
    timerInterval = null,
    hardStop = false;

function animateSquares(element) {
    $(element)
        .animate({
            'background-color':'#22CC22',
            boxShadow:'0 0 20px #00ff00'
        }, 600)
        .animate({
            'background-color':'#FF66B3',
            boxShadow:'0 0 20px #f0f'
        }, 600, function(){(animateSquares(element))}); 
}

function timerSetup() {
    seconds = 0;
    $('.timer')
        .css('width','100vw')
        .css('background-color','#22cc22')
        .stop();
    if (timerInterval !== undefined) {
        timerInterval = setInterval(countdown, 100);
    }
}

function countdown() {
    if (hardStop === false) { //setInterval is being a pain
        $('.timer')
            .animate({'width':'-=1vw'},{duration: 50})
            .animate({'background-color':'#ff0000'},{duration: 3000, queue: false});
        seconds += 1;
        score -= 1;
        console.log(seconds);
        if (seconds > 100) {
            giveUp();
            stopTimer();
        }
    }
}

function stopTimer() {
    clearInterval(timerInterval);
    timerInterval = null;
}

function checkEnter() {
    if(event.key === 'Enter' && wrong === false && correct === false) {
        userSubmit();
    }
}

function generateWordList() { //word list from https://github.com/dwyl/english-words/blob/master/words_alpha.txt
    $.get('fiveLetterWords.txt', function(data) {
        fiveLetters = data.split(/\r?\n/);
        pickWord();
    });
}

function pickWord() {
    randomWordID = Math.floor(Math.random() * 2000);
    randomWord = fiveLetters[randomWordID];
    console.log(randomWord);
    
    chars = randomWord.split('');
    $(".word-line:nth-child(1) .letter:nth-child(1)").text(chars[0]);
    timerSetup();
}

function userClickBox() {
    $('#warning-box').hide();
}

function userSubmit() {
    guess += 1;
    hits = 0;
    wordChars = [];
    toColour = [];
    var submission = $('#answer').val().toLowerCase(),
        fail = false;

    // ERRORS
    if (submission.length == 0) {
        $('#warning-box').text("You didn't enter a word!");
        $('#warning-box').show();
        fail = true;
        guess -= 1;
    } else if (submission.length < 5) {
        $('#warning-box').html("The word <span class='submission'>" + submission + "</span> is too short! Must be five letters.");
        $('#warning-box').show();
        fail = true;
        guess -= 1;
    } else if (!fiveLetters.includes(submission)) {
        wrong = true;
    }
    
    if (fail === false) {
        timerSetup();
    }
    
    // IF THERE ARE NO ERRORS...
    // This is the bulk of the code
    
    if (fail === false) {
        var submissionChars = submission.split('');
        letterMatchesThisCycle = [];
        
        // IF SUCCESSFUL, we don't need to loop through the letters - you've already won
        if (chars.join() == submissionChars.join()) {
            correct = true;
            for (var i=0;i<5;i++) {
                let j = i + 1;
                let m = $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")");
                animateSquares(m);
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")")
                    .text(submissionChars[i])
                    .addClass("green");
            }
            for (var i=0;i<6;i++) {
                if (i !== guess){
                    $("tr.word-line:nth-child(" + i + ")").animate({'opacity':'20%'},600);
                }
            }
            $('#warning-box').html("<strong>CONGRATULATION!</strong><br /><br /><strong>" + score + " POINTS!</strong><br /><br />The word was <span class='submission'>" + randomWord + "</span>!<br /><br />(<a href='https://en.wiktionary.org/wiki/" + randomWord + "' target='_blank'>WTF does that mean?</a>)");
            $("#main-area").animate({'background-color':'#157A15'},600);
            $('#warning-box').show();
            $('#restart').show();
            disableButtons();
            hardStop = true;
        }
        
        // If you didn't get it right, you either had a wrong guess or it wasn't a word.
        
        for (var i=0;i<5;i++) {
            var j = i + 1,
                guess2 = guess + 1;
            
            // If you're out of guesses...
            if (guess == 5 && correct === false) {
                let j = i + 1;
                for (var n=0;n<6;n++) {
                    if (n !== 5) {
                        $("tr.word-line:nth-child(" + n + ")").animate({'opacity':'20%'},600);
                    }
                }
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").text(submissionChars[i]);
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").text(chars[i]);
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").addClass("red");
                $('#warning-box').html("<strong>GAME OVER YEAH!</strong><br /><br />The word was <span class='submission'>" + randomWord + "</span>!<br /><br />(<a href='https://en.wiktionary.org/wiki/" + randomWord + "' target='_blank'>WTF does that mean?</a>)");
                $("#main-area").animate({'background-color':'#7A1515'},600);
                $('#warning-box').show();
                $('#restart').show();
                disableButtons();
                hardStop = true;
            }
            
            // If the word isn't in the dictionary...
            if (wrong === true && guess !== 5) {
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").text(submissionChars[i]);
                $("tr.word-line:nth-child(" + guess2 + ") td.letter:nth-child(" + j + ")").text(chars[i]);
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").addClass("black");
                $("tr.word-line:nth-child(" + guess2 + ") td.letter:nth-child(" + j + ")").addClass("red");
                $("#main-area").animate({'background-color':'#7A1515'},600);
                for (var n=0;n<6;n++) {
                    if (n !== guess2) {
                        $("tr.word-line:nth-child(" + n + ")").animate({'opacity':'20%'},600);
                    }
                }
                
            /*    for (var n=0;n<6;n++) {
                    if (n !== guess) {
                        $("tr.word-line:nth-child(" + guess + ")").animate({'opacity':'20%'},600);
                    }
                } */
                
                $('#warning-box').html("The word <span class='submission'>" + submission + "</span> isn't in the dictionary.<br /><br />The word was <span class='submission'>" + randomWord + "</span>!<br /><br />(<a href='https://en.wiktionary.org/wiki/" + randomWord + "' target='_blank'>WTF does that mean?</a>)");
                $('#warning-box').show();
                $('#restart').show();
                disableButtons();
                hardStop = true;
                
            // now, if your guess is a word...
            
            } else if (wrong === false && guess !== 5) {
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").text(submissionChars[i]);
                
                // If it's green
                if (submissionChars[i] == chars[i]) {
                    if (correct === false) {
                        $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").addClass("green");
                        letterMatches[i] = submissionChars[i];
                        letterMatchesThisCycle.push(submissionChars[i]);
                        hits += 1; // add 1 here if there's a match, so we know which match is best
                    }
                } 
                
                if (correct === false) {
                    $("tr.word-line:nth-child(" + guess2 + ") td.letter:nth-child(" + j + ")").text(letterMatches[i]);
                }
            }
        }
        
        // another loop for the yellow check, since some words might erraneously have a yellow where the green exists already
        
        var unguessedLetters = [];
        
        for (var i=0;i<5;i++) {
            unguessedLetters.push(chars[i]);
        }
        
        for (var k=0;k<letterMatchesThisCycle.length;k++) {
            let index = unguessedLetters.indexOf(letterMatchesThisCycle[k]);
            if (index > -1) {
                unguessedLetters.splice(index, 1);
            }
        }
        
        for (var i=0;i<5;i++) {
            
            if (correct === false) {
                let j = i + 1;
                
                if (!letterMatchesThisCycle.includes(submissionChars[i]) && unguessedLetters.includes(submissionChars[i])) {
                    toColour.push(j);
                    let index = unguessedLetters.indexOf(submissionChars[i]);
                    if (index > -1) {
                        unguessedLetters.splice(index, 1);
                    }
                    
                }
                
            }
        }
        
        for (var i=0;i<5;i++) {
            let j = i + 1;
            
            if (toColour.includes(j)) {
                $("tr.word-line:nth-child(" + guess + ") td.letter:nth-child(" + j + ")").addClass("yellow");
            }
        }
    if (fail === false) {    
        stopTimer();
    }
    }
    
    // other stuff
    $('#answer').val('');
    $('#answer').focus();
}

function giveUp() {
    let guess2 = guess + 1;
    
    for (var i=0;i<5;i++) {
        let j = i + 1;
        $("tr.word-line:nth-child(" + guess2 + ") td.letter:nth-child(" + j + ")").text(chars[i]);
        $("tr.word-line:nth-child(" + guess2 + ") td.letter:nth-child(" + j + ")").addClass("red");
    }
    
    for (var i=0;i<6;i++) {
        if (i !== guess2){
            $("tr.word-line:nth-child(" + i + ")").animate({'opacity':'20%'},600);
        }
    }
    
    $('#warning-box').html("The word was <span class='submission'>" + randomWord + "</span>!<br /><br />(<a href='https://en.wiktionary.org/wiki/" + randomWord + "' target='_blank'>WTF does that mean?</a>)");
    $("#main-area").animate({'background-color':'#7A1515'},600);
    $('#warning-box').show();
    $('#restart').show();
    disableButtons();
    hardStop = true;
}

function restart() {
    location.reload();
}

function disableButtons() {
    let submitButton = document.querySelector('#submit');
    let giveupButton = document.querySelector('#give-up');
    let inputBox = document.querySelector('#answer');
    submitButton.disabled = true;
    giveupButton.disabled = true;
    inputBox.disabled = true;
}

$(document).ready(function() {
    generateWordList();
    $('#answer').focus();
});
