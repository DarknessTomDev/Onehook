# PixelPlaceJS
Fully documented and strongly typed nodejs libary for PixelPlace.io


## Using the library

To install the library run `npm install pixelplacejs`

Proceed to Usage section


## Developing the library

This is only required for developers

1. Clone the repo `git clone https://github.com/DarknessTomDev/PixelPlaceJS`
2. Install packages by running `npm install`
3. Run `npm run run-dev` to start PixelPlaceJS.

## Usage

### Listen for events using the `world` module


#### Javascript

```js

const { World, EPackets } = require("pixelplacejs")

(async () => {

    const CANVAS_ID = 7;

    let world = new World(CANVAS_ID);
    await world.Init();

    world.on(EPackets.NEW_CHAT_MESSAGE, (message) => {
        console.log(`${message.username}: ${message.message}`)
    })

    console.log("PP is running")
})()

```

#### Typescript

```ts

import { World, EPackets, Types } from 'pixelplacejs'

(async () => {

    const CANVAS_ID = 7;

    let world = new World(CANVAS_ID);
    await world.Init();

    world.on(EPackets.NEW_CHAT_MESSAGE, (message: Types.Chat.ChatMessage) => {
        console.log(`${message.username}: ${message.message}`)
    })

    console.log("PP is running")
})()

```

### Use one or more bots to draw an image

```ts

import { World, PixelPlace, Auth } from 'pixelplacejs'

(async () => {

    const CANVAS_ID = 7;

    let accounts: Auth[] = [
        new Auth(null, {
            authId: "", //Fill these values
            authKey: "",
            authToken: ""
        })
    ]

    let world = new World(CANVAS_ID);
    await world.Init();
    console.log("World is ready!")

    let pp = new PixelPlace(accounts, world, CANVAS_ID);
    await pp.Init();
    console.log("PP is ready!")

    let [x, y] = [1336, 1839];
    await pp.render.drawImage({x, y}, "test.png", 200, true);

})()


```

### Render Public Functions

```ts
Render.drawImage(position: IVector2D, imagePath: string, size: number, protect: boolean = false): Promise<IImageData>
Render.drawRect(position: IVector2D, size: IVector2D, color: number): Promise<void>
```

### PixelPlace Public Functions

```ts
PixelPlace.Init(): Promise<void>
PixelPlace.RegisterProtectionZone(startX: number, startY: number, original: IImageData): void
PixelPlace.placePixel(x: number, y: number, color: number): Promise<Boolean>
```


### Utils

PixelplaceJS also lets you access various of utility methods.

```js
const { Utils } = require("pixelplacejs");
const fs = require("fs");

(async () => {
    const CANVAS_ID = 7;
    let canvasBuffer = Utils.getLatestCanvasPNG(CANVAS_ID);
    let pixelplaceColor = Utils.getColorFromRGB(255, 255, 255);
    let palive = Utils.generatePingAlive();

    fs.writeFileSync(canvasBuffer, "map.png");
    console.log(`White's PixelPlace color ID is: ${pixelplaceColor}`);
    console.log(`Valid palive at the current second is ${palive()}`);
})()


```


## Contact

For any help, issues or general contact, you can reach out to me on my discord: `_.shuffle._`