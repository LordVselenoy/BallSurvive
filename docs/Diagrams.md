classDiagram
    %% Основные классы игры
    class Game {
        -gameState: GameState
        -player: Player
        -obstacles: Obstacle[]
        -score: number
        -time: number
        +start(): void
        +update(): void
        +render(): void
        +checkCollisions(): boolean
        +gameOver(): void
    }

    class Player {
        -position: Vector2
        -radius: number
        -color: string
        +move(direction: Vector2): void
        +draw(ctx: CanvasRenderingContext2D): void
    }

    class Obstacle {
        <<abstract>>
        +position: Vector2
        +width: number
        +height: number
        +color: string
        +draw(ctx: CanvasRenderingContext2D): void
        +update(speed: number): void
    }

    class BlueStripe {
        -speed: number
        +draw(ctx: CanvasRenderingContext2D): void
        +update(): void
    }

    class Vector2 {
        +x: number
        +y: number
        +add(v: Vector2): Vector2
        +multiply(scalar: number): Vector2
    }

    class GameState {
        <<enumeration>>
        MENU
        PLAYING
        GAME_OVER
    }

    %% Взаимосвязи между классами
    Game "1" *-- "1" Player : contains
    Game "1" *-- "n" Obstacle : contains
    BlueStripe --|> Obstacle : inherits
    Player "1" *-- "1" Vector2 : position
    Obstacle "1" *-- "1" Vector2 : position
    Game "1" *-- "1" GameState : state