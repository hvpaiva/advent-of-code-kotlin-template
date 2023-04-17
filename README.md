# Advent of Code Kotlin Template

[Advent of Code][aoc] – an annual event in December since 2015.
Every year since then, with the first day of December, a programming puzzles contest is published every day for twenty-four days.
A set of Christmas-oriented challenges provide any input you have to use to answer using the language of your choice.
We offer you a template prepared to use it with [Kotlin][kotlin] language within this repository.

> This template is inspired by the [Jetbrains one][original-template]. But heavily modified to fit my needs.

![][file:cover]

## Workflow
**Advent of Code Kotlin Template** is a particular type of GitHub repository that lets you speed up the setup phase and 
start writing your AoC solutions immediately.

The general idea is straightforward – to create a new project based on this template, you need to log in to your GitHub 
account and use the **Use this template** green button.
And remember – **do not fork it!**

After creating a new project based on this template in your account, a dedicated GitHub Actions workflow will start and 
clean up the code from redundant files.
It will also personalize code to use your username and project name in namespaces and Gradle properties.
How cool is that?

Right after the [@actions-user][actions-user] actor pushes the second commit to your repository, you're ready to 
clone it within the IntelliJ IDEA.

From now, everything's in your hands!
Join the [Advent of Code][aoc] contest, solve the Day O1 as soon as it is published.

For the following days, copy the `day01` solution folder and increment the day number.
Or you can use the [tip](#tip) below.

> Remember to join the Kotlin contest!
> 
> To do that, edit your project's _About_ section with ⚙️ icon and add the `aoc-2022-in-kotlin` topic to your project.
> 
> **We will find your repository and count you in our giveaway.** 

## Content

After you create a new project based on the current template repository using the **Use this template** button, a 
bare minimal scaffold will appear in your GitHub account with the following structure:

```
.
├── README.md                   README file
├── build.gradle.kts            Gradle configuration created with Kotlin DSL
├── gradle
│   └── wrapper                 Gradle Wrapper
├── gradle.properties           Gradle configuration properties
├── gradlew                     *nix Gradle Wrapper script
├── gradlew.bat                 Windows Gradle Wrapper script
├── settings.gradle.kts         Gradle project settings
└── src
    ├── day01
    │   ├── Day01.kt            An empty implementation for the first AoC day
    │   ├── Day01.txt           An file for the Day 01 input data
    │   └── Day01_test.txt      An Day 01 test input data used for checks
    ├── DayPuzzle.kt            The abstraction for the AoC day puzzle
    └── Utils.kt                A set of utility methods shared across your days
```

> Note: All task input files are excluded from the repository with `.gitignore` – we should not post them publicly, 
> as Eric Wastl asks for: [Tweet](https://twitter.com/ericwastl/status/1465805354214830081).

```kotlin
fun main() {
    DayPuzzle<Int>("01")
        .withParts(Part1, Part2)
        .solve()
}
```

The `DayPuzzle` class is a generic class that accepts the day number as a string and provides a set of methods to
configure the puzzle and solve it.

The `withParts` method accepts a list of `Part` implementations that are responsible for the puzzle part solution.
It also allows you to only execute the tests with a parameter in the `solve` method:

```kotlin
fun main() {
    DayPuzzle<Int>("01")
        .withParts(Part1, Part2)
        .solve(onlyTests = true)
}
```

In the `solve` method,
you can also specify which parts you want to solve by passing its names in varargs `partNames` parameter:

```kotlin
fun main() {
    DayPuzzle<Int>("01")
        .withParts(Part1, Part2)
        .solve(onlyTests = true, "Part 2")
}
```

Besides the main function you will find a `Part` implementation for each puzzle part. 
Each part is responsible for calculating the solution for the given input data. 
It'll receive the input data as a list of strings and should return
the solution as the type defined in `DayPuzzle` type receiver.

```kotlin
object Part1 : DayPuzzle.PartPuzzle<Int>("Part 1", 24000) {
    override fun solve(input: List<String>): Int {
        return 0
    }
}
```

The `PartPuzzle` class is a generic abstract class that accepts the part `name`, 
that will be used for better output visualization and to filter the parts that will be solved (if needed),
and the `valueTestExpected` that is the expected value for the test input data.

The `solve` method is the one that should be implemented by the `Part` implementation.

The `input` parameter is the data loaded from the `src/day01/Day01.txt` file 
and from the `src/day01/Day01_test.txt` file. 
And each line of the input file is a separate element in the list.

This input data is common for both parts, and you can find it on the bottom of each 
day on the [Advent of Code][aoc] page.

By running the main function, you will see the following output:

```bash
Test Part 1: 7 OK
Part 1: 1647
Test Part 2 Failed. Expecting 19 but was 13
Part 2: 2447
```

The tests are performed against the `valueTestExpected` value, and if the test fails, 
the expected and actual values are printed to the console.

The actual solution is printed after the test. 
Make sure to check if the test is correct before submitting your solution to the contest.

The `Part` implementations are independent of each other, so you can solve them in any order you want.
And you even can solve only one part of the puzzle.
Or more than two.
It's up to you.

## Getting help

If you stuck with Kotlin-specific questions or anything related to this template, check out the following resources:

- [Kotlin docs][docs]
- [Kotlin Slack][slack]
- Template [issue tracker][issues]

## Tip

You can create a File and Code Template in IntelliJ IDEA to create a new day folder with all the necessary files.

1. Go to **Settings** > **Editor** > **File and Code Template**.
2. Click the **+** button.
3. Enter the **Name** (a suggestion "AoC Day") and **Extension** `kt`.
4. In the file name field, enter `${NAME.toLowerCase()}/${NAME}`.
5. Paste the following code into the **Template text** field:

```kotlin
#parse("File Header.java")
package ${NAME.toLowerCase()}

import DayPuzzle

fun main() {
    DayPuzzle<Int>("${NAME.substring(3, 5)}")
        .withParts(Part1)
        .solve()
}

data object Part1 : DayPuzzle.PartPuzzle<Int>("Part 1", 10) {
    override fun solve(input: List<String>): Int {
        return input.size
    }
}
```

6. _(Optional)_ You can add the text files as well
   - Create a new nested template by clicking the icon right to the **+** button _(an icon with a file and plus image)_.
   - Put in the name `${NAME.toLowerCase()}/${NAME}` and extension `txt`.
   - Paste anything into the **Template text** field. It's not really important as you will override in the puzzle solving.
7. _(Optional)_ Repeat step 6 for the test file, naming it `${NAME.toLowerCase()}/${NAME}_test`.


> To use is just right-click on the `src` folder and select **New** > **AoC Day**. 
> And put the day name in the **Name** field. 
> Like `Day02`
> _(It's case-insensitive, but need to have the word 'day' with its number (with left zero) without the space,
> because IntelliJ don't handle well just passing the number)_.

[actions-user]: https://github.com/actions-user
[aoc]: https://adventofcode.com
[docs]: https://kotlinlang.org/docs/home.html
[original-template]: https://github.com/kotlin-hands-on/advent-of-code-kotlin-template
[issues]: https://github.com/hvpaiva/advent-of-code-kotlin-template
[kiss]: https://en.wikipedia.org/wiki/KISS_principle
[kotlin]: https://kotlinlang.org
[slack]: https://surveys.jetbrains.com/s3/kotlin-slack-sign-up
[file:cover]: .github/readme/cover.png
[file:utils]: src/Utils.kt
