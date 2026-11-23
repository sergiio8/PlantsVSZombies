# Plants vs. Zombies (Terminal Simulation)

A Java command-line simulation inspired by *Plants vs. Zombies*. Defend a
4 × 8 board by placing plants, collecting sun, and surviving progressively
harder zombie waves. The project demonstrates object-oriented design,
command parsing, turn-based game updates, and score-record persistence.

This is an academic project developed by
[Sergio Martínez Olivera](https://github.com/sergiio8) and
[Daniel Roldán Serrano](https://github.com/danirold).

## Features

- Deterministic games through an optional random seed.
- Three difficulty levels: `EASY`, `HARD`, and `INSANE`.
- Four playable plants: Sunflower, Peashooter, Wall-Nut, and Cherry-Bomb.
- Four zombie types: Zombie, BucketHead, Sporty, and Explosive Zombie.
- Sun collection, suncoin spending, plant attacks, zombie movement, and
  cycle-based updates.
- Persistent per-level high scores in `record.txt`.
- Input validation and help/list commands for the terminal interface.

## Requirements

- Java Development Kit (JDK) 15 or newer. The source uses
  `String.formatted(...)`, introduced in Java 15.
- A POSIX-compatible shell for the commands below.

The original coursework submission is preserved as
[`coursework/plants-vs-zombies/archive/Entrega3SergioyDaniel.zip`](coursework/plants-vs-zombies/archive/Entrega3SergioyDaniel.zip).
It does not include Maven or Gradle build metadata.

## Build and run

From the repository root, extract the archive and enter the extracted project
directory:

```sh
unzip coursework/plants-vs-zombies/archive/Entrega3SergioyDaniel.zip
cd Entrega3SergioyDaniel-5
```

Compile the production sources:

```sh
rm -rf out
mkdir out
javac -d out $(find src -name '*.java' ! -path '*/p3/pruebas/*')
```

Start a game by passing a difficulty level and, optionally, a seed:

```sh
java -cp out tp1.p2.PlantsVsZombies EASY 25
```

Supported levels are `EASY`, `HARD`, and `INSANE`. Omitting the seed uses a
time-based seed, while supplying one makes the random sequence reproducible.
Run the command from the extracted project root so the game can read and
write `record.txt`.

## Controls

Type `help` in the game to print the command list. The main commands are:

| Command | Purpose |
| --- | --- |
| `add <plant> <col> <row>` | Buy and place a plant |
| `catch <col> <row>` | Collect a sun |
| `none` or an empty line | Skip the player action for one cycle |
| `list` / `listZombies` | Show available plants / zombies |
| `record` | Show the current level record |
| `reset` | Restart the current game |
| `reset <level> <seed>` | Restart with explicit settings |
| `exit` | Leave the game |

The `addZombie` and `cheatPlant` commands are included by the original
project for testing and demonstration purposes.

## Architecture

The source is organised under the `tp1` package:

- `tp1.p2` contains the application entry point.
- `tp1.p2.control` parses commands, validates parameters, and coordinates
  input.
- `tp1.p2.logic` owns game state, cycles, resources, zombies, records, and
  world updates.
- `tp1.p2.logic.gameobjects` contains plant, zombie, and sun entities plus
  their factories.
- `tp1.p2.view` renders the board and user-facing messages.
- `tp1.p3.pruebas` contains the original JUnit-based output tests.

## Testing

The archive includes JUnit 5 test sources under `src/tp1/p3/pruebas`, but no
build file or JUnit dependency is bundled. The tests also expect text fixtures
under `test/p3/` (including `00-easy_25-input.txt`,
`00-easy_25-expected.txt`, and `00-easy_25-output.txt`) that are not present in
the archive. Consequently, the tests cannot run from this submission as
provided. Running them requires both the missing fixture set and JUnit 5
dependencies, configured on the test class path. The production compile
command above intentionally excludes the JUnit test sources.

## Project status

This repository preserves the original educational submission under
`coursework/plants-vs-zombies/archive/`. The project is a working terminal-game
prototype rather than a packaged desktop or web game; the ZIP layout and
manual Java compilation are part of the current project format.

## License

Distributed under the [MIT License](LICENSE).
