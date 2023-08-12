<script>
import "./styles.css";
// import { onMount } from "svelte/internal";
import Phaser from "phaser";





// Set the width of your game in px
let CanvasWidth = 800;

// Set the height of your game in px
let CanvasHeight = 600;

let character;
let background;
let cursors;


class MyGame extends Phaser.Scene {
    constructor() {
        super();
    }

    // Preload img assets before adding them to the game screen
    preload() {
        this.load.multiatlas("cityscene", "assets/spritesheets/cityscene.json", "assets/spritesheets");
    }

    // Add all needed assets to the game scene
    create() {
        // background
        background = this.add.sprite(0, 0, "cityscene", "background.png");

        // sprite
        character = this.add.sprite(10, 400, "cityscene", "capguy/walk/0001.png");
        character.setScale(0.5, 0.5);

        // animation
        const frameNames = this.anims.generateFrameNames("cityscene", {
            start: 1, end: 8, zeroPad: 4,
            prefix: "capguy/walk/", suffix: ".png"
        });

        this.anims.create({ key: "walk", frames: frameNames, frameRate: 10, repeat: -1 });
        cursors = this.input.keyboard.createCursorKeys();
    }

    // Loop that checks for events to fire specified functions
    update() {
        if (cursors.left.isDown) {
            moveLeft();
        } else if (cursors.right.isDown) {
            moveRight();
        }
        else {
            stopAnim();
        }
    }
}

const config = {
    type: Phaser.AUTO,
    width: CanvasWidth,
    height: CanvasHeight,
    scene: MyGame
};

// Initializing the game
const game = new Phaser.Game(config);





function moveLeft() {
    // console.log("Left move");
    character.x -= 3;
    character.anims.play("walk", true);
}

function moveRight() {
    // console.log("Right move");
    character.x += 3;
    character.anims.play("walk", true);
}

function stopAnim() {
    // console.log("Halt");
    character.anims.play("walk", false);
}
    
</script>

<svelte:head>
	<title>Game</title>
	<meta name="description" content="Game" />
</svelte:head>

<style>

</style>
