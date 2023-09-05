# Getting feedback from our automated tests

Many of the assignments in this course have automated tests (also known as "specs") built in. They come in two forms:

- from a Codespace to our Grades interface via the `rake grade` bash prompt command when building an app
- from our graded code blocks found within our Ruby lessons

This lesson covers both of these, and will teach you how to interpret the automated feedback you receive from our tests.

## Grades within an app assignment: `rake grade`

When you load an assignment from one of our lessons by click the "Load [Project Name] assignment" button, you will be taken to the Grades interface. There, you can click the top link to fork the assignment and setup a Codespace. Gitpod and Local setup instructions are also available, but we recommend sticking with Codespaces.

Whichever environment you use to setup the VSCode workspace, you will need to copy and paste the token from the Grades interface into your bash prompt the first time you run `rake grade` to get feedback from our automated tests.

**Remember that your first job is always to make your app work as described and test it manually yourself. If there is a target app, use that for reference. Debug your live app preview by Reading The Error Messages. You should not rely exclusively on the automated tests; they are a terrible way to debug.** 

When you're ready for feedback, try this command at your bash prompt (i.e. not in the terminal tab running the live app preview server):

```
rake grade
```

You'll be asked for your access token. If you have closed the Grades interface, just click the "Load [Project Name] assignment" button again to reopen it and view the token. Copy-paste the token from the Grades page into your bash prompt after the `>`. This only needs to be done one time, and then the token will be stored in that workspace:

<!-- ![](/assets/grades-token.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1686005312/grades-token_vyb9cy.png)

You will get a pop up window in the Codespace workspace asking for permission to paste from your clipboard into the workspace, you should "Allow" this action.

<!-- ![](assets/grades-token-enter.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1686008287/grades-token-enter_wf7s8y.png)

You should see output that looks like:

<!-- ![](assets/grades-token-submission-url.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1686008310/grades-token-submission-url_lc4mpf.png)

Copy-paste the Results URL into a new tab, or <kbd>Cmd</kbd> + click (Mac) / <kbd>Ctrl</kbd> + click (Windows) on it. (Select "Trust grades.firstdraft.com" in the dialog that comes up.)

This will take you to a "build report" with the results of our automated tests for the project:

---

<!-- ![](/assets/rake-grade-build-report.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1689969155/rake-grade-build-report_dgbzj3.png)
{: .bleed-full }

---

If you click on a test, you will find some additional feedback. That might include some hints (in this case about matching the copy in the target app exactly):

---

<!-- ![](assets/rake-grade-results-details.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1689971541/rake-grade-results-details_ytfao4.png)
{: .bleed-full }

---

You can also click on the "Examine test" button, which will take you to the actual Ruby of the automated test on the `appdev-projects/<project-name>` GitHub repo that is within our `spec/` folder on every app we assign:

---

<!-- ![](assets/rake-grade-rspec-on-github.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1689970235/rake-grade-rspec-on-github_zja6vk.png)
{: .bleed-full }

---

It's surprisingly readable! Ruby's testing gem `rspec` uses method names that are supposed to make tests readable even for non-technical managers and clients. You can see specifically what flow is being tested and what inputs are being used and what the expected output is, and try to reproduce the issue in your own app manually using the same inputs.

You can run `rake grade` in your terminal as many times as you want, and you will get a new updated build report each time. It will only report your highest score back to Canvas!

## Sidenote 1: Resetting your token

Ever put in the wrong token to a project? For instance, you put in the token from the `hello-world` Grades interface into the `links` Codespace when you ran `rake grade` the first time.

You can just run

```
rake grade:reset
```

at the bash prompt to reset it and then re-enter the correct token the next time you `rake grade`.

## Sidenote 2: whitespace and case sensitivity with "regular expressions"

In some of our tests you might notice odd patterns in our expectations:

<!-- ![](assets/rake-grade-whitespace-regex.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1689970373/rake-grade-whitespace-regex_n9ens3.png)
{: .bleed-full }

These are so-called "regular expressions" and every programming language has them; often in exactly the same format. If you want to learn more about these powerful tools, I recommend the [regexone tutorial](https://regexone.com/). 

We will learn more about these in the Ruby lessons, but for now let me break it down for you:

```ruby
/Welcome\s+to\s+Rock-Paper-Scissors/i
```

* the first and last forward slashes `/` identify the start and stop of the expression to search for
* everything between the forward slashes is the pattern that the test is seeking to match
* anything that begins with a backslash `\` is an "escape character"; in this case `\s` means "whitespace"
* things after the escape character modify them further; in this case the `+` after the `\s`'s means "one or more whitespace"
* finally, the `i` after the last forward slash means "case insensitive"

Why did we go through all this trouble?

Because we want you as a beginner to have an easier time with our tests; small typos in the copy are easy to make and often hard to catch without some experience. We want all three of these versions of the copy you might write in the `<h1>` tag for this test to pass:

- What is shown in the test title and target app:
    ```
    Welcome to Rock-Paper-Scissors
    ```
- An extra space or two you accidentally add:
    ```
    Welcome  to  Rock-Paper-Scissors
    ```
- The wrong case for some characters:
    ```
    Welcome  to  rock-paper-scissors
    ```

Without our regular expression matcher, only the first of these would pass!

## Grades within our Ruby lessons: graded code blocks

When you get to our Ruby lessons, you will find interactive graded code blocks built right into the page.

When you click the "Run" button on those tests, you are again making sure the code you wrote passes some automated tests that we wrote. If the test fails, you'll see a bunch of output that looks like this:

---

![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1687363037/graded-code-block-test-fails_efx6ga.png)
{: .bleed-full } 

---

This output is not particularly beginner-friendly, but it is what the output of an automated test looks like in the real world, and developers spend all day reading output like this. In fact, this is what the the raw output from our `rake grade` command in your Codespace projects looks like; we just turn it into a beginner friendly format in our Grades interface. 

(We're working on making the graded code block results here more readable — stay tuned.)

If the test passes, you should see output like this:

---

![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1687363106/graded-code-block-test-passes_yyrzhe.png)
{: .bleed-full }

---
