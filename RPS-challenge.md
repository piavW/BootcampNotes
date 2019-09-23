# Rock - Paper- Scissors Challenge Career training - tech interview

**Very important challenge for the letter of recommendation - do your best and the sky's the limit!**

During first interview you get a challenge, then a few days later you have a new meeting where you go over the solution and explain it. 

Solo-programming!

- 14 days to complete the tech-challenge.
- During that time you check-in with your coach and tell them about your progress, potential blockers etc. 
- Friday in 2 weeks we demo the solution. 

OK to just bring llgic, ok to bring a fully styled application, ok to game against the computer, randomise usin rand-method with randomized computer input, ok to make it possible to be 2 players in the same game.

In 1st interview: describe your general plan - language, libraries, testdriven, work agile? - functioning code above all else.... for the solution. 

In 2nd - talk through the solution, blockers & solution, classes, components? Demo the thing. I deviate from 1st meeting plans, tell why. 

It's hard to test randomize methods in unit and feature testing. There's a workaround. We can ask Thomas for help if it's super specific. 

Make a draft of approach!
tests written first, committed, then implementation. 
---

## Draft for 1st interview:

- Work agile/eXtreme Programming by using
    - Behaviour and Test Driven Development
    - refactoring
    - continuous integration
    - continuous deployment
But the main focus is working software where the player can challenge the computer. Styling and adding multiple player-interactivitiy will be a secondary concern. 

- Code in vanilla JavaScript
- unit and feature/acceptance testing with NodeJs and chai assertion library and Cucumber
- I'll use continuous deployment to my github and to the soon-to-be-deployed webbased interface. That way I can deliver the code in small instances. 

Implementation:
- Writing tests first. 
- Switch-case-statement for rock, paper, scissor functionality where the value of each instance is declared as more than or less than the other.
- A randomize method for what the computer chooses. Stub out.... 

time management! Plan ur fucking time. 

If use any onlinesources, tutuorials, github - reference them in the readme "inspired by ..."
In readme - simple setup explination of npm, yarn etc. (if you clone repo make sure you do npm install..)

Keep Noel updates as if he was an employer through Slack - when I have something cool to show. 




// Copy of application.features cause we don't need to featuretest with both cucumber and e2e2. 
require('../spec.helper');

context('User can click on one of 3 buttons and see a result of who won.', () => {
  before(async () => {
    await browser.init()
    await browser.visitPage('http://localhost:8080/')
  });

  beforeEach(async () => {
    await browser.page.reload();
  });

  after(() => {
    browser.close();
  });

  it('User can see the page titel', async () => {
    expect(await browser.page.title()).to.eql('Rock Paper Scissors');
  });

  it('User can see three buttons', async () => {
    expect(await browser.page.button()).to.eq('Rock', 'Paper', 'Scissors');
  });
  
  //Below is WIP
  // it ('User can click on a button and see who won', async () => {
  //   await browser.clickOnButton("input[value='Check']")
  //   let content = await browser.getContent("[id='display_answer']")
  //   expect(content).to.eql('Rock wins');
  //   })

});


     When("I click button with {string}", function(string){
        // Write code here that turns the phrase above into concrete actions
        return "pending";
    });

        <header>Header</header>
    <main>
        <button type="submit">Rock</button>
        <button type="submit">Paper</button>
        <button type="submit">Scissors</button>
    </main>
    <footer>Footer</footer>
    '

     describe('Computer chooses at random', () => {})

app.js under playerChoice

      if (document.getElementById("Rock").addEventListener("click", playerRock)) {
            let playerChoice = rock

index.html
<button id="Rock" onclick="playerRock" type="button">Rock</button>
        <button onclick="playerPaper" type="button" >Paper</button>
        <button onclick="playerScissor" type="button">Scissors</button>
    </main>

RANDOM! 
randItem returns a random item from an array, randPick removes a random item from an array, and randPut puts a item at a random position in an array. And a seeded random (Not as good as Math.random but more than enough for most applications) 